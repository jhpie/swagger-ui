# swagger-ui
스웨거 ui확인을 위한 테스트 코드

# 실행화면
![image](https://user-images.githubusercontent.com/77376346/163744327-9f26043b-1e70-4d18-8fd0-252a2ba8c953.png)

# maven dependencies
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>3.0.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>3.0.0</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-boot-starter</artifactId>
            <version>3.0.0</version>
        </dependency>

# SwaggerConfig ( + @Configuration /@EnableSwagger2 추가 )
    # ApiInfo
    # swagger-ui의 title 및 description 정의
    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
                .title("my_swagger_title")
                .description("API EX")
                .build();
    }
    # Docket - Swagger 설정의 핵심으로 문서화객체이다
    @Bean
    public Docket api(){
        return new Docket(DocumentationType.SWAGGER_2)
                .groupName("test") # 그룹이름
                .apiInfo(this.apiInfo()) # API INFO
                .select() # ApiSelectorBuilder생성
                .apis(RequestHandlerSelectors.any()) # 컨트롤러가 존재하는 패키지를 기본패키지로 지정하여 requestMapping이 선언된 api를 문서화
                .paths(PathSelectors.any()).build(); # path 조건에 해당하는 api 선택
    }
