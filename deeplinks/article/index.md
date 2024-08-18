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

```sh
apt update && apt install certbot
certbot certonly -d flythere-deeplink.egortarasov.com
```