
<a href="http://loopback.io"><img src="loopback-logo-sm.png"></a>

##  Setup

To preview the website locally:

1. Install [Ruby and Bundler](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/) if you don't have them already.

1. Clone this repo (you might use the SSH URL instead of HTTPS):

```
git clone https://github.com/strongloop/loopback.io.git
```

3. `cd` to the repository directory and run the following command:
```
$ cd loopback.io
$ bundle install
```

Bundler will look

## Some markdown 

Here is an HTML table.

<table>
  <thead>
    <tr>
    <th width="150">Property</th>
    <th width="80">Type</th>
    <th>Description</th>
    </tr>
  </thead> 
  <tbody>
    <tr>
      <td>connector</td>
      <td>String</td>
      <td>Connector name, either “loopback-connector-mongodb” or “mongodb”.</td>  
    </tr>  
    <tr>
      <td>database</td>
      <td>String</td>
      <td>Database name</td> 
      </tr>
    <tr>
      <td>host</td>
      <td>String</td>
      <td>Database host name</td>
    <tr>
      <td>password</td>
      <td>String</td>
      <td>Password to connect to database</td> 
    </tr>
    <tr>
      <td>port</td>
      <td>Number</td>
      <td>Database TCP port</td> 
    </tr>
    <tr>
      <td>url</td>
      <td>String</td>
      <td>Connection URL of form <code>mongodb://user:password@host/db</code>.  
      Overrides other connection settings (see below).</td> 
    </tr>
    <tr>
       <td>username</td> 
       <td>String</td>
       <td>Username to connect to database</td>
    </tr>
</tbody>
</table>

## Second heading

Here is a markdown table.

Property&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Type    | Description
---------------| --------| --------
database       | String  | Database name
schema         | String  | Specifies the default schema name that is used to qualify unqualified database objects in dynamically prepared SQL statements. The value of this property sets the value in the CURRENT SCHEMA special register on the database server. The schema name is case-sensitive, and must be specified in uppercase characters
username       | String  | DB2 Username
password       | String  | DB2 password associated with the username above
hostname       | String  | DB2 server hostname or IP address
port           | String  | DB2 server TCP port number
useLimitOffset | Boolean | LIMIT and OFFSET must be configured on the DB2 server before use (compatibility mode)
supportDashDB  | Boolean | Create ROW ORGANIZED tables to support dashDB.

