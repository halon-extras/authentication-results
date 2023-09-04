## Authentication-Results Header Field 
Add a Authentication-Results Header Field (https://tools.ietf.org/html/rfc7001).

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-authentication-results
```

### RHEL

```
yum install halon-extras-authentication-results
```

## Example

```
import { dmarc } from "extras://dmarc";
import { AuthenticationResults } from "extras://authentication-results";

$spf = spf_query($connection["remoteip"], $connection["helo"]["host"], $transaction["senderaddress"]["domain"]);
$dmarc = dmarc($arguments["mail"], $connection["remoteip"], $connection["helo"]["host"], $transaction["senderaddress"]["domain"]);

$arguments["mail"]->addHeader("Authentication-Results",
    AuthenticationResults()
    ->SPF($spf, $connection["helo"]["host"], $transaction["senderaddress"]["domain"], ["smtp.remote-ip" => $connection["remoteip"]])
    ->DKIM($arguments["mail"])
    ->DMARC($dmarc)
    ->toString(gethostname()),
    ["encode" => false]
);
```
