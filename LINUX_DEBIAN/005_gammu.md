# Servicio de mensajeria masiva SMS

## Instalaciones previas

Instalar modem-manager-gui para las pruebas de envio de mensajes y verificacion de funcionamiento del modem

    $ sudo apt-get install modem-manager-gui
    $ modem-manager-gui

Instalar wvdial monitor de puertos usb dialout

   $ sudo apt-get install wvdial

Identificar puerto de los modems

   $ sudo wvdialconf

    ```
    tyUSB16<*1>: ATQ0 V1 E1 -- OK
    ttyUSB16<*1>: ATQ0 V1 E1 Z -- OK
    ttyUSB16<*1>: ATQ0 V1 E1 S0=0 -- OK
    ttyUSB16<*1>: ATQ0 V1 E1 S0=0 &C1 -- OK
    ttyUSB16<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 -- OK
    ttyUSB16<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0 -- COMMAND NOT SUPPORT
    ttyUSB16<*1>: Modem Identifier: ATI -- Manufacturer: huawei
    ttyUSB16<*1>: Speed 9600: AT -- OK
    ttyUSB16<*1>: Max speed is 9600; that should be safe.
    ttyUSB16<*1>: ATQ0 V1 E1 S0=0 &C1 &D2 -- OK

    Found a modem on /dev/ttyUSB3.
    Modem configuration written to /etc/wvdial.conf.
    ttyUSB3<Info>: Speed 9600; init "ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0"
    ttyUSB13<Info>: Speed 9600; init "ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0"
    ttyUSB14<Info>: Speed 9600; init "ATQ0 V1 E1 S0=0 &C1 &D2"
    ttyUSB16<Info>: Speed 9600; init "ATQ0 V1 E1 S0=0 &C1 &D2"

    ```
## Instalar gammu

Instalacion

   $ sudo apt-get install gammu gammu-smsd
   $ sudo apt-get install -f
   $ sudo apt-get install gammu gammu-smsd
   $ gammu --version

Levantar demonio gammu

   $ sudo apt-get /etc/init.d/gammu-smsd status

Desinstalar gammu

   $ sudo apt-get remove --purge gammu
   $ sudo apt-get remove --purge gammu-smsd
   $ sudo apt-get clean


Configurar gammu

   $ sudo gammu-config
   ```
   ...
   port : /dev/ttyUSB3
   connection = at
   ...
   -> save
   ```
   or

   $ sudo nano /root/.gammurc

Verificar configuracion

   $ sudo gammu --identify

   ```
   Dispositivo          : /dev/ttyUSB14
   Fabricante           : Huawei
   Modelo               : unknown (E303)
   Firmware             : 21.158.13.00.677
   IMEI                 : 867575004580174
   IMSI de la SIM       : 736010901716189
   ```
Enviar mensaje de texto

   $ sudo gammu sendsms text 59172067615

    Introduzca el texto del mensaje y pulse Ctrl+D:
    Nuevo envio de mensaje gammu
    Si quiere cancelar, pulse Ctrl+C...
    Enviando SMS 1/1...esperando respuesta de la red..Aceptar, referencia de mensaje=17

  # sudo gammu sendsms TEXT 59172067615 -text "Hola mundo gammu"

Ver mensajes leidos

    $ sudo gammu getallsms

# configuracion de archivos ssh servidor remoto

    Modem numero 76271015

    $ ssh -l jmamani 192.168.21.100
    password: ******

    $ sudo chown jmamani:desarrollo -R /opt/



# Integracion con Postgres Backend

ejecutar el siguiente script como pgScriptSql

```
--
-- Database: "smsd"
--
-- CREATE USER "smsd" WITH NOCREATEDB NOCREATEUSER;
-- CREATE DATABASE "smsd" WITH OWNER = "smsd" ENCODING = 'UTF8';
-- \connect "smsd" "smsd"
-- COMMENT ON DATABASE "smsd" IS 'Gammu SMSD Database';

-- --------------------------------------------------------

--
-- Function declaration for updating timestamps
--
CREATE LANGUAGE plpgsql;
CREATE OR REPLACE FUNCTION update_timestamp() RETURNS trigger AS $update_timestamp$
  BEGIN
    NEW."UpdatedInDB" := LOCALTIMESTAMP(0);
    RETURN NEW;
  END;
$update_timestamp$ LANGUAGE plpgsql;

-- --------------------------------------------------------

--
-- Sequence declarations for tables' primary keys
--

--CREATE SEQUENCE inbox_ID_seq;

--CREATE SEQUENCE outbox_ID_seq;

--CREATE SEQUENCE outbox_multipart_ID_seq;

--CREATE SEQUENCE sentitems_ID_seq;

-- --------------------------------------------------------

--
-- Index declarations for tables' primary keys
--

--CREATE UNIQUE INDEX inbox_pkey ON inbox USING btree ("ID");

--CREATE UNIQUE INDEX outbox_pkey ON outbox USING btree ("ID");

--CREATE UNIQUE INDEX outbox_multipart_pkey ON outbox_multipart USING btree ("ID");

--CREATE UNIQUE INDEX sentitems_pkey ON sentitems USING btree ("ID");

-- --------------------------------------------------------

--
-- Table structure for table "gammu"
--

CREATE TABLE gammu (
  "Version" smallint NOT NULL DEFAULT '0' PRIMARY KEY
);

--
-- Dumping data for table "gammu"
--

INSERT INTO gammu ("Version") VALUES (16);

-- --------------------------------------------------------

--
-- Table structure for table "inbox"
--

CREATE TABLE inbox (
  "UpdatedInDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "ReceivingDateTime" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "Text" text NOT NULL,
  "SenderNumber" varchar(20) NOT NULL DEFAULT '',
  "Coding" varchar(255) NOT NULL DEFAULT 'Default_No_Compression',
  "UDH" text NOT NULL,
  "SMSCNumber" varchar(20) NOT NULL DEFAULT '',
  "Class" integer NOT NULL DEFAULT '-1',
  "TextDecoded" text NOT NULL DEFAULT '',
  "ID" serial PRIMARY KEY,
  "RecipientID" text NOT NULL,
  "Processed" boolean NOT NULL DEFAULT 'false',
  CHECK ("Coding" IN
  ('Default_No_Compression','Unicode_No_Compression','8bit','Default_Compression','Unicode_Compression'))
);

--
-- Dumping data for table "inbox"
--

-- --------------------------------------------------------

--
-- Create trigger for table "inbox"
--

CREATE TRIGGER update_timestamp BEFORE UPDATE ON inbox FOR EACH ROW EXECUTE PROCEDURE update_timestamp();

-- --------------------------------------------------------

--
-- Table structure for table "outbox"
--

CREATE TABLE outbox (
  "UpdatedInDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "InsertIntoDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "SendingDateTime" timestamp NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "SendBefore" time NOT NULL DEFAULT '23:59:59',
  "SendAfter" time NOT NULL DEFAULT '00:00:00',
  "Text" text,
  "DestinationNumber" varchar(20) NOT NULL DEFAULT '',
  "Coding" varchar(255) NOT NULL DEFAULT 'Default_No_Compression',
  "UDH" text,
  "Class" integer DEFAULT '-1',
  "TextDecoded" text NOT NULL DEFAULT '',
  "ID" serial PRIMARY KEY,
  "MultiPart" boolean NOT NULL DEFAULT 'false',
  "RelativeValidity" integer DEFAULT '-1',
  "SenderID" varchar(255),
  "SendingTimeOut" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "DeliveryReport" varchar(10) DEFAULT 'default',
  "CreatorID" text NOT NULL,
  "Retries" integer DEFAULT '0',
  "Priority" integer DEFAULT '0',
  CHECK ("Coding" IN
  ('Default_No_Compression','Unicode_No_Compression','8bit','Default_Compression','Unicode_Compression')),
  CHECK ("DeliveryReport" IN ('default','yes','no'))
);

CREATE INDEX outbox_date ON outbox("SendingDateTime", "SendingTimeOut");
CREATE INDEX outbox_sender ON outbox("SenderID");

--
-- Dumping data for table "outbox"
--

-- --------------------------------------------------------

--
-- Create trigger for table "outbox"
--

CREATE TRIGGER update_timestamp BEFORE UPDATE ON outbox FOR EACH ROW EXECUTE PROCEDURE update_timestamp();

-- --------------------------------------------------------

--
-- Table structure for table "outbox_multipart"
--

CREATE TABLE outbox_multipart (
  "Text" text,
  "Coding" varchar(255) NOT NULL DEFAULT 'Default_No_Compression',
  "UDH" text,
  "Class" integer DEFAULT '-1',
  "TextDecoded" text DEFAULT NULL,
  "ID" serial,
  "SequencePosition" integer NOT NULL DEFAULT '1',
  PRIMARY KEY ("ID", "SequencePosition"),
  CHECK ("Coding" IN
  ('Default_No_Compression','Unicode_No_Compression','8bit','Default_Compression','Unicode_Compression'))
);

--
-- Dumping data for table "outbox_multipart"
--


-- --------------------------------------------------------

--
-- Table structure for table "phones"
--

CREATE TABLE phones (
  "ID" text NOT NULL,
  "UpdatedInDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "InsertIntoDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "TimeOut" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "Send" boolean NOT NULL DEFAULT 'no',
  "Receive" boolean NOT NULL DEFAULT 'no',
  "IMEI" varchar(35) PRIMARY KEY NOT NULL,
  "IMSI" varchar(35) NOT NULL,
  "NetCode" varchar(10) DEFAULT 'ERROR',
  "NetName" varchar(35) DEFAULT 'ERROR',
  "Client" text NOT NULL,
  "Battery" integer NOT NULL DEFAULT -1,
  "Signal" integer NOT NULL DEFAULT -1,
  "Sent" integer NOT NULL DEFAULT 0,
  "Received" integer NOT NULL DEFAULT 0
);

--
-- Dumping data for table "phones"
--

-- --------------------------------------------------------

--
-- Create trigger for table "phones"
--

CREATE TRIGGER update_timestamp BEFORE UPDATE ON phones FOR EACH ROW EXECUTE PROCEDURE update_timestamp();

-- --------------------------------------------------------

--
-- Table structure for table "sentitems"
--

CREATE TABLE sentitems (
  "UpdatedInDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "InsertIntoDB" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "SendingDateTime" timestamp(0) WITHOUT time zone NOT NULL DEFAULT LOCALTIMESTAMP(0),
  "DeliveryDateTime" timestamp(0) WITHOUT time zone NULL,
  "Text" text NOT NULL,
  "DestinationNumber" varchar(20) NOT NULL DEFAULT '',
  "Coding" varchar(255) NOT NULL DEFAULT 'Default_No_Compression',
  "UDH" text NOT NULL,
  "SMSCNumber" varchar(20) NOT NULL DEFAULT '',
  "Class" integer NOT NULL DEFAULT '-1',
  "TextDecoded" text NOT NULL DEFAULT '',
  "ID" serial,
  "SenderID" varchar(255) NOT NULL,
  "SequencePosition" integer NOT NULL DEFAULT '1',
  "Status" varchar(255) NOT NULL DEFAULT 'SendingOK',
  "StatusError" integer NOT NULL DEFAULT '-1',
  "TPMR" integer NOT NULL DEFAULT '-1',
  "RelativeValidity" integer NOT NULL DEFAULT '-1',
  "CreatorID" text NOT NULL,
  CHECK ("Status" IN
  ('SendingOK','SendingOKNoReport','SendingError','DeliveryOK','DeliveryFailed','DeliveryPending',
  'DeliveryUnknown','Error')),
  CHECK ("Coding" IN
  ('Default_No_Compression','Unicode_No_Compression','8bit','Default_Compression','Unicode_Compression')),
  PRIMARY KEY ("ID", "SequencePosition")
);

CREATE INDEX sentitems_date ON sentitems("DeliveryDateTime");
CREATE INDEX sentitems_tpmr ON sentitems("TPMR");
CREATE INDEX sentitems_dest ON sentitems("DestinationNumber");
CREATE INDEX sentitems_sender ON sentitems("SenderID");

--
-- Dumping data for table "sentitems"
--

-- --------------------------------------------------------

--
-- Create trigger for table "sentitems"
--

CREATE TRIGGER update_timestamp BEFORE UPDATE ON sentitems FOR EACH ROW EXECUTE PROCEDURE update_timestamp();


```
