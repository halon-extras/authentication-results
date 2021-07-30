## Authentication-Results Header Field 
Add a Authentication-Results Header Field (https://tools.ietf.org/html/rfc7001).

```
import { AuthenticationResults } from "authentication-results/authentication-results.hsl";

$arguments["mail"]->addHeader("Authentication-Results",
    AuthenticationResults()
    ->SPF($connection["remoteip"], $connection["helo"]["host"], $transaction["senderaddress"]["domain"], ["smtp.remote-ip" => $connection["remoteip"]])
    ->DKIM($arguments["mail"])
    ->DMARC()
    ->toString(),
    ["encode" => false]
);
```
