### FAQ

```text
Q:
2022-04-23 18:46:16.347  WARN 1580 --- [nio-9000-exec-2] org.keycloak.events                      : type=LOGIN_ERROR, realmId=springseeds, clientId=client1, userId=null, ipAddress=127.0.0.1, error=invalid_redirect_uri, redirect_uri=http://localhost:4200/

A:
在访问/openid-connect/token接口时出现上述错误。需要设置client1客户端的Root URL，Valid Redirect URIs， Base URL属性，如：Valid Redirect URIs设置为http://localhost:4200/* ，注意必须带*号。
```

![divider](./divider.png)

```text
Q:
2022-04-23 18:43:19.969  WARN 1580 --- [nio-9000-exec-5] org.keycloak.events                      : type=INTROSPECT_TOKEN_ERROR, realmId=springseeds, clientId=client1, userId=null, ipAddress=127.0.0.1, error=invalid_request, detail='Client not allowed.', client_auth_method=client-secret

A:
在访问/token/introspect接口时出现上述错误。需要设置client1客户端属性Access Type=confidential, Web Orgins=+
```

![divider](./divider.png)

```text
Q:
2022-04-23 19:24:22.979  WARN 1580 --- [io-9000-exec-11] org.keycloak.events                      : type=CODE_TO_TOKEN_ERROR, realmId=springseeds, clientId=client1, userId=null, ipAddress=127.0.0.1, error=invalid_client_credentials, grant_type=authorization_code

A:
在访问/openid-connect/token接口时出现上述错误。可能是client1客户端密码不对，检查客户端credentials标签的Secret属性。
```

![divider](./divider.png)

```text
Q:
访问http://localhost:9000/auth/realms/springseeds/account/，使用一般用户登录，出现forbidden

A:
进入你的realm，Client Scopes -> roles -> Mappers -> client roles 查看 Token Claim Name 项目，我先前修改过此项目，正确的配置应该是：resource_access.${client_id}.roles ，之前设置是：resource_access.roles
```

![divider](./divider.png)