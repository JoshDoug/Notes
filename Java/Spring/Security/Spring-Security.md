# [Spring Security](https://spring.io/projects/spring-security)

* [Spring Security Current Docs](https://docs.spring.io/spring-security/site/docs/current/reference/html5/)

## Introduction

### 1. Prerequisites

### 2. Spring Security Community

### 3. What's New in Spring Security

### 4. Getting Spring Security

### 5. Features

### 6. Project Modules and Dependencies

Lots of modules!

### 7. Samples

## Servlet Applications

### 8. Hello Spring Security

#### 8.1 Updating Dependencies

#### 8.2 Starting Hello Spring Security Boot

#### 8.3 Spring Boot Auto Configuration

Spring Boot automatically:

* Enables Spring Security's default config, this creates a servlet `Filter` as a bean named `springSecurityFilterChain`. This bean is responsible for all the security within the application, such as protecting application URLs, validating submitted username and passwords, redirecting to the log in form, etc.
* Creates a `UserDetailsService` bean with a username of `user` and a randomly generated password that is logged to the console when starting the application.
* Registers the `springSecurityFilterChain` servlet filter bean (is that what it is?) with the Servlet container for every request - TKTK I suppose this is why Hibernate many-to-many relationships didn't work properly as it was within the Servlet container lifecycle instead of Spring's Application Context?

This means an authenticated user is required for any interaction with the application by default.

### 9. Servlet Security: The Big Picture

#### 9.1 A Review of Filters

#### 9.2 DelegatingFilterProxy

#### 9.3 FilterChainProxy

#### 9.4 SecurityFilterChain

#### 9.5 [Security Filters](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#servlet-security-filters)

A long list of Security Filters, although we're probably most interested in UsernamePasswordAuthenticationFilter, DigestAuthenticationFilter, BasicAuthenticationFilter, ExceptionTranslationFilter, FilterSecurityInterceptor

#### 9.6 Handling Security Exceptions

### 10. Authentication

#### 10.1 SecurityContextHolder

#### 10.2 SecurityContext

#### 10.3 Authentication

#### 10.4 GrantedAuthority

#### 10.5 AuthenticationManager

#### 10.6 ProviderManager

#### 10.7 AuthenticationProvider

#### 10.8 Request Credentials with AuthenticationEntryPoint

AuthenticationEntryPoint - normally redirects to a login form, but how does that work with a SPA?
Do we just return an unauthorised/forbidden (unauthorised probably makes more sense?) and let the SPA handle the redirect?

#### 10.9

#### 10.10

#### 10.11

### 11. Authorization

#### 11.1 Authorization Architecture

##### 11.1.1 Authorities

##### 11.1.2 Pre-Invocation Handling

##### 11.1.3 After Invocation Handling

##### 11.1.4 Hierarchical Roles

#### 11.2 Authorize HttpServletRequest with FilterSecurityInterceptor

#### 11.3 Expression-Based Access Control

#### 11.4 Secure Object Implementations

#### 11.5 Method Security

#### 11.6 Domain Object Security (ACLs)

### 12. OAuth2

## Reactive Applications

### 22. WebFlux Security

### 23. Protection Against Exploits

### 24. OAuth2 WebFlux

### 25. @RegisteredOAuth2AuthorizedClient
