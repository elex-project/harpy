# Project Harpy

HTTP Companion

```kotlin
repositories {
	mavenCentral()
	maven {
		name = "Github Packages"
		url = uri("https://maven.pkg.github.com/elex-project/harpy")
		credentials {
			username = project.findProperty("github.username") as String
			password = project.findProperty("github.token") as String
		}
	}
}
```

for projects with Java 9+, please consider using New Http Client, instead of HttpRequest in this package.

```java
try {
    HttpGetRequest<String> request = new HttpGetRequest<>(
            Uri.builder()
            .scheme("https").host("www.elex-project.com")
            .build());
    request.setFollowRedirect(true);
    request.send(new HttpStringResponseHandler() {
        @Override
        public void onResponse(final int status, final Map<String, List<String>> headers,
                               @Nullable final String message) {
            Console.writeLine("Status: {}",status);
            for (String key : headers.keySet()) {
                try {
                    Console.writeLine("Header: {} = {}", key, headers.get(key));
                } catch (Throwable ignore) {
                }
            }
            Console.writeLine(message);
        }

        @Override
        public void onException(final Throwable e) {
            e.printStackTrace();
        }
    });


} catch (IOException e) {
    e.printStackTrace();
}
```

---
developed by Elex
https://www.elex-project.com
