## Authentication-Results Header Field 
Add a Authentication-Results Header Field (https://tools.ietf.org/html/rfc7001).

```
import { AuthenticationResults } from "authentication-results/authentication-results.hsl";

$mail->addHeader("Authentication-Results", AuthenticationResults()
				->SPF(["smtp.remote-ip" => $senderip])
				->DKIM()
				->DMARC()
				->toString()
		);
```
