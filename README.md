# loopback-example-connector (SOAP)

The SOAP connector enables LoopBack applications to interact with
[SOAP](http://www.w3.org/TR/soap)-based web services described using
[WSDL](http://www.w3.org/TR/wsdl).  This example app illustrates calling a [periodic table SOAP web service](http://www.webservicex.net/periodictable.asmx) from a LoopBack app,
where you define a remote method to call each SOAP web service operation.
This is a simple example of a LoopBack app "proxying" or intermediating a web service.

For more information, see the
<a href="http://loopback.io/doc/en/lb3/SOAP-connector.html">SOAP connector</a> documentation.

## Installation

Clone this repo and install dependencies from npm:


```shell
$ git clone https://github.com/strongloop-community/loopback-example-connector.git -b soap
$ cd loopback-example-connector
$ npm install
```

## Run the example

1. In the project root directory, run the app by entering this command:
    ```
    node .
    ```

    You'll see this in the console:
    ```
    Web server listening at: http://0.0.0.0:3000
    Browse your REST API at http://0.0.0.0:3000/explorer
    ```

2. Open [API Explorer](http://0.0.0.0:3000/explorer) in your web browser.  
3. Under the **periodicTable** model, you'll see two endpoints: `GET /periodicTables/GetAtomicNumber` and `GET /periodicTables/GetAtomicWeight`.  
1. Click on `GetAtomicNumber` and in the **elementName** parameter field, enter the name of an element, for example, "Gold" or "Oxygen".  

In the **Response Body** field, you'll see an XML response from the web service that looks something like this:
    ```
    {
    "GetAtomicNumberResult": "<NewDataSet>\r\n  <Table>\r\n    <AtomicNumber>26</AtomicNumber>\r\n    <ElementName>Iron</ElementName>\r\n    <Symbol>Fe</Symbol>\r\n    <AtomicWeight>55.847</AtomicWeight>\r\n    <BoilingPoint>3300</BoilingPoint>\r\n    <IonisationPotential>7.9</IonisationPotential>\r\n    <EletroNegativity>1.6400000000000001</EletroNegativity>\r\n    <AtomicRadius>1.17</AtomicRadius>\r\n    <MeltingPoint>1808</MeltingPoint>\r\n    <Density>7874</Density>\r\n  </Table>\r\n</NewDataSet>"
    }
    ```

### Additional example code

The app includes two other files `periodictable-ws.js` and `stock-ws.js` that illustrate other ways of programmatically calling a SOAP web service.  NOTE: the [stock quote web service](http://www.webservicex.net/stockquote.asmx) may not be consistenly available.

## Recreating the app

**Prerequisites**: Follow the steps in the [Installation documentation](http://loopback.io/doc/en/lb3/Installation.html) to install the LoopBack CLI.  In a nutshell:
```
$ npm install -g loopback-cli
```

To create this app yourself, follow the steps in this section.


## Scaffold the app

Scaffold a new application.  Enter this command:

```
$ lb app
```

When prompted, respond as follows:
- `? What's the name of your application?` Give the app any name you wish, for example "my-soap-demo".
The tool will create a directory with that name (`my-soap-demo`).
- `? Enter name of the directory to contain the project:` Press Enter to accept the default (directory has the same name as the app).
- `? Which version of LoopBack would you like to use?` Choose `3.x (current)`
- `? What kind of application do you have in mind?` Choose `empty-server (An empty LoopBack API, without any configured models or datasources) `

The tool will then scaffold the app and install all the dependencies from npm.

Go into the app root directory:
```
$ cd my-soap-demo
```

## Create a SOAP data source

Use the [data source generator](http://loopback.io/doc/en/lb3/Data-source-generator.html) to add a SOAP data source to your application.  Enter this command:

```shell
$ lb datasource
```

You'll see this prompt:
```
? Enter the datasource name:
```

Enter "soapDS".

For this prompt:
```
? Select the connector for soapDS:
```
Use your arrow key to scroll down to `SOAP webservices (supported by StrongLoop)` and press Enter.

For this prompt:
```
? URL to the SOAP web service endpoint:
```

Copy and paste the URL of the periodic table web service:
```
http://www.webservicex.net/periodictable.asmx
```

For this prompt:
```
? HTTP URL or local file system path to the WSDL file:
```

Copy and paste this URL of the periodic table web service WSDL:
```
http://www.webservicex.net/periodictable.asmx?WSDL
```

For this prompt:
```
? Expose operations as REST APIs: (Y/n)
```

Press Enter to accept the default (yes).

For this prompt:
```
? Maps WSDL binding operations to Node.js methods:
```

Copy and paste this stringified JSON:
```
{"getAtomicWeight":{"service":"periodictable","port":"periodictableSoap","operation":"GetAtomicWeight"},"getAtomicNumber":{"service":"periodictable","port":"periodictableSoap","operation":"GetAtomicNumber"}}
```

NOTE: The JSON you enter must **not** have any line endings, that is, it must be on a single line.

For this prompt:
```
? Install loopback-connector-soap@^3.0
```

Press Enter.

The data source generator then creates an entry for the data source in the `server/datasources.json` file and installs all the necessary dependencies.

## Create a periodicTable model

Use the [model generator](http://loopback.io/doc/en/lb3/Model-generator.html) to add a model to represent the periodic Table web service.  Enter this command:

```shell
$ lb model
```

When prompted, respond as follows:

- `Enter the model name:`  Enter "periodicTable".
- `Enter the model name: periodicTable` Select `soapDS` that you previously created.
- `? Select model's base class` Select `Model`.
- `? Expose periodicTable via the REST API? (Y/n)`  Press Enter to accept the default (yes).
- `? Custom plural form (used to build REST URL):` Press Enter for no custom plural.
- `? Common model or server only?` Select `server` because this will be a server-only model.
- `? Property name:` Press Enter when first prompted, because this model will not have any properties.

The tool will create two files in the `server` directory: `periodicTable.json` and `periodicTable.js`.

## Add remote methods

Edit `server/models/periodic-table.js` and add the code shown below to the stubbed-out function.

This code defines two functions, `Periodictable.getAtomicnumber` and `Periodictable.getAtomicweight` and adds them as remote methods to the `Periodictable` model, as described in [Remote methods]
(https://loopback.io/doc/en/lb3/Remote-methods.html).

```javascript
'use strict';

module.exports = function(Periodictable) {

  // External PeriodTable WebService operation exposed as REST APIs through LoopBack
  Periodictable.getAtomicnumber = function (elementName, cb) {
    Periodictable.GetAtomicNumber({ElementName: elementName || 'Copper'}, function (err, response) {
      var result = response;
      cb(err, result);
    });
  };

  // External PeriodTable WebService operation exposed as REST APIs through LoopBack
  Periodictable.getAtomicweight = function(elementName, callback) {
    Periodictable.GetAtomicWeight({ElementName: elementName || 'Copper'}, function (err, response) {
      var result = response;
      callback(err, result);
    });
  }

  // Map to REST/HTTP
  Periodictable.remoteMethod(
      'getAtomicnumber', {
        accepts: [
          {arg: 'elementName', type: 'string', required: true,
            http: {source: 'query'}}
        ],
        returns: {arg: 'result', type: 'object', root: true},
        http: {verb: 'get', path: '/GetAtomicNumber'}
      }
  );

  Periodictable.remoteMethod(
      'getAtomicweight', {
        accepts: [
          {arg: 'elementName', type: 'string', required: true,
            http: {source: 'query'}}
        ],
        returns: {arg: 'result', type: 'object', root: true},
        http: {verb: 'get', path: '/GetAtomicWeight'}
    }
  );

};
```
