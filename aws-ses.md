## AWS SES 이용하여 이메일 보내기(Draft)

## gradle
```groovy
compile group: 'com.amazonaws', name: 'aws-java-sdk-ses', version: "${awsSesVersion}"
```

## AWS SES Configuration
```java
/**
 * @author Heo, Jin Han
 * @since 2018-05-02
 */
@Configuration
public class AwsSesConfig {

  @Value("${AWS_ACCESS_KEY_ID}")
  private String AWS_ACCESS_KEY_ID;

  @Value("${AWS_SECRET_KEY}")
  private String AWS_SECRET_KEY;

  @Bean
  public AmazonSimpleEmailServiceAsync amazonSimpleEmailService() {
    BasicAWSCredentials basicAWSCredentials = new BasicAWSCredentials(AWS_ACCESS_KEY_ID, AWS_SECRET_KEY);

    return AmazonSimpleEmailServiceAsyncClient.asyncBuilder()
        .withCredentials(new AWSStaticCredentialsProvider(basicAWSCredentials))
        .withRegion(Regions.US_WEST_2)
        .build();
  }
}

```

## SendEmailRequest Factory Class 필요
- SendEmailRequest를 만들때 편리하게 하기 위한 Factory Class 필요

## HTML Format
- 2가지 방법
- AWS SES Create Template으로 등록해놓고 쓰기
- SpringTemplateEngine을 이용해서 HTML to String으로 만들어서 쓰기