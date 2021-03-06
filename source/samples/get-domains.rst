
.. code-block:: bash

    curl -s --user 'api:YOUR_API_KEY' -G \
	https://api.mailgun.net/v3/domains \
	-d skip=0 \
	-d limit=3

.. code-block:: java

 import javax.ws.rs.client.Client;
 import javax.ws.rs.client.ClientBuilder;
 import javax.ws.rs.client.Entity;
 import javax.ws.rs.client.WebTarget;

 import javax.ws.rs.core.Form;
 import javax.ws.rs.core.MediaType;

 import org.glassfish.jersey.client.authentication.HttpAuthenticationFeature;

 public class MGSample {

     // ...

     public static ClientResponse GetDomains() {

         Client client = ClientBuilder.newClient();
         client.register(HttpAuthenticationFeature.basic(
             "api",
             "YOUR_API_KEY"
         ));

         WebTarget mgRoot = client.target("https://api.mailgun.net/v3");

         return mgRoot
             .path("/domains")
             .queryParam("skip", 0)
             .queryParam("limit", 3)
             .request()
             .buildGet()
             .invoke(ClientResponse.class);
     }
 }

.. code-block:: php

  # Include the Autoloader (see "Libraries" for install instructions)
  require 'vendor/autoload.php';
  use Mailgun\Mailgun;

  # Instantiate the client.
  $mgClient = new Mailgun('YOUR_API_KEY');

  # Issue the call to the client.
  $result = $mgClient->get("domains", array('limit' => 5, 'skip' => 10));

.. code-block:: py

 def get_domains():
     return requests.get(
         "https://api.mailgun.net/v3/domains",
         auth=("api", "YOUR_API_KEY"),
         params={"skip": 0,
                 "limit": 3})

.. code-block:: rb

 def get_domains
   RestClient.get "https://api:YOUR_API_KEY"\
   "@api.mailgun.net/v3/domains", :params => {
     :skip => 0,
     :limit => 3
   }
 end

.. code-block:: csharp

 using System;
 using System.IO;
 using RestSharp;
 using RestSharp.Authenticators;
 
 public class GetDomainsChunk
 {
 
     public static void Main (string[] args)
     {
         Console.WriteLine (GetDomains ().Content.ToString ());
     }
 
     public static IRestResponse GetDomains ()
     {
         RestClient client = new RestClient ();
         client.BaseUrl = new Uri ("https://api.mailgun.net/v3");
         client.Authenticator =
             new HttpBasicAuthenticator ("api",
                                         "YOUR_API_KEY");
         RestRequest request = new RestRequest ();
         request.Resource = "domains";
         request.AddParameter ("skip", 0);
         request.AddParameter ("limit", 3);
         return client.Execute (request);
     }
 
 }

.. code-block:: go

 func GetDomains(domain, apiKey string) (int, []mailgun.Domain, error) {
   mg := mailgun.NewMailgun(domain, apiKey, "")
   return mg.GetDomains(-1, -1)
 }
