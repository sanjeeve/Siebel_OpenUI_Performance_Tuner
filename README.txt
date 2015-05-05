##Siebel OpenUI WebServer Performance Tuning
===========================================

According to Oracle the below settings should be done in Siebel OpenUI enviornment

- Minify customization by using a tool such as YUI Compressor for your custom JavaScript and CSS.
- Enable Gzip compression on the Web server.
- Disable entity tags (ETags) on the Web server. Doing this generally improves performance on multi-server deployments.
- Set header expiration to five days for production deployments. Do not set header expiration for development environments.

## Enable Gzip compression on the Web server.
Make the following changes in web.config (iis root)

...
<httpCompression
      directory="%SystemDrive%\inetpub\temp\IIS Temporary Compressed Files">
   <scheme name="gzip" dll="%Windir%\system32\inetsrv\gzip.dll" />
   <dynamicTypes>
      <add mimeType="text/*" enabled="true" />
      <add mimeType="message/*" enabled="true" />
      <add mimeType="application/x-javascript" enabled="true" />
      <add mimeType="application/json" charset="utf-8" enabled="true" /> 
  <add mimeType="application/json" enabled="true" />    
  <add mimeType="*/*" enabled="false" />
   </dynamicTypes>
   <staticTypes>
      <add mimeType="text/*" enabled="true" />
      <add mimeType="message/*" enabled="true" />
      <add mimeType="application/x-javascript" enabled="true" />
      <add mimeType="application/xaml+xml" enabled="true" />
   <add mimeType="*/*" enabled="false" />
   </staticTypes>
</httpCompression>
...

## Disable entity tags (ETags) on the Web server. Doing this generally improves performance on multi-server deployments.

..
I've written an IIS module for this, please download the solution OUIWebServerTuner 
..

## Set header expiration to five days for production deployments. Do not set header expiration for development environments.
..
I've tried this within config but it doesn't seem to be working, so I included the header expiry code within the same OUIWebServerTuner solution.
..