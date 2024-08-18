```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Deeplink Playground',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Deeplink Playground'),
        ),
        body: const Center(
          child: Text(
            'Hello, Deeplinks!',
          ),
        ),
      )
    );
  }
}
```

```sh
nslookup flythere-deeplink.egortarasov.com
```

```sh
apt update && apt install certbot
certbot certonly --standalone -d flythere-deeplink.egortarasov.com
```

```sh
curl https://$DEEPLINK_HOST/
```

```sh
curl https://$DEEPLINK_HOST/.well-known/apple-app-site-association
```

```conf
server {
    listen [::]:443 ssl ipv6only=on;
    listen 443 ssl;

    ssl_certificate /etc/letsencrypt/live/$DEEPLINK_HOST/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/$DEEPLINK_HOST/privkey.pem;
    
    location = / {
        default_type application/json;
        return 200 '{ "Hello" : "FromNginx" }';
    }
}
```

```sh
code ~/.bashrc
```

```sh
export DEEPLINK_HOST=flythere-deeplink.egortarasov.com
```

```yaml
services:
  nginx:
    image: nginx
    environment:
      - HOST=${DEEPLINK_HOST}
    volumes:
      - ./default.conf.template:/etc/nginx/templates/default.conf.template
      - /etc/letsencrypt:/etc/letsencrypt
      - ./apple-app-site-association.json:/etc/nginx/html/.well-known/apple-app-site-association
    ports:
      - "443:443"
```

`default.conf.template`:

```conf
server {
    listen [::]:443 ssl ipv6only=on;
    listen 443 ssl;

    ssl_certificate /etc/letsencrypt/live/$HOST/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/$HOST/privkey.pem;
}
```


```sh
docker compose up -d
```

```sh
curl https://$DEEPLINK_HOST/
```

```
195.20.239.227
```

```sh
open ios/Runner.xcodeproj
```

```
Runner -> Signing & Capabilities > Bundle Identifier
com.example.flythereDeeplinks

Runner -> Signing & Capabilities > Signing Certificate (98Y5P8S823)
98Y5P8S823

Result:
98Y5P8S823.com.example.flythereDeeplinks
```