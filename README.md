# Java code for access the api


      import okhttp3.*;
      
      import java.io.IOException;
      import java.time.Instant;
      
      
      public class Main {
      
          public static void main(String[] args) throws IOException {
      
              OkHttpClient client = new OkHttpClient();
      
              MediaType mediaType = MediaType.parse("application/json");
              RequestBody body = RequestBody.create(mediaType, "\"{\\\"operator\\\":311,\\\"canumber\\\":DL12CB4685}\"");
              Request request = new Request.Builder()
                      .url("https://sit.paysprint.in/service-api/api/v1/service/fastag/Fastag/fetchConsumerDetails")
                      .post(body)
                      .addHeader("accept", "application/json")
                      .addHeader("Token", getToken())
                      .addHeader("Content-Type", "application/json")
                      .build();
      
              Response response = client.newCall(request).execute();
              System.out.println(response);
          }
          private static int getRandom() {
              int random = (int) Math.round(Math.random() * 1000000000);
              return random;
          }
      
          private static long getTimestamp() {
              long timestamp = Instant.now().getEpochSecond();
              return timestamp;
          }
      
          public static String getToken() {
              int random = getRandom();
              long timestamp = getTimestamp();
              String secretKey = io.jsonwebtoken.impl.TextCodec.BASE64.encode("UFMwMDEyNGQ2NTliODUzYmViM2I1OWRjMDc2YWNhMTE2M2I1NQ==");
              String token = io.jsonwebtoken.Jwts.builder()
                      .setIssuer("PSPRINT")
                      .setHeaderParam("typ", "JWT")
                      .setHeaderParam("alg", "HS256")
                      .claim("iss", "PSPRINT")
                      .claim("timestamp", timestamp)
                      .claim("partnerId", "PS001773")
                      .claim("product","FASTAG")
                      .claim("reqid", random)
                      .signWith(io.jsonwebtoken.SignatureAlgorithm.HS256, secretKey)
                      .compact();
      
              return token;
          }
      }


# In console :

      11:38:49 am: Executing ':Main.main()'...
      
      
      > Task :compileJava
      
      > Task :processResources NO-SOURCE
      > Task :classes
      Note: C:\Users\prade\OneDrive\Desktop\jwt\src\main\java\org\example\Main.java uses or overrides a deprecated API.
      Note: Recompile with -Xlint:deprecation for details.
      
      > Task :Main.main()
      Response{protocol=h2, code=401, message=, url=https://sit.paysprint.in/service-api/api/v1/service/fastag/Fastag/fetchConsumerDetails}
      
      Deprecated Gradle features were used in this build, making it incompatible with Gradle 9.0.
      
      You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.
      
      For more on this, please refer to https://docs.gradle.org/8.5/userguide/command_line_interface.html#sec:command_line_warnings in the Gradle documentation.
      
      BUILD SUCCESSFUL in 1s
      2 actionable tasks: 2 executed
      11:38:51 am: Execution finished ':Main.main()'.


It comes with 401 code. what I did wrong ?
