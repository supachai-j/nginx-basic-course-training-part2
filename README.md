# NGINX Basic Course Training Part 2
## เนื้อหา:
1. Setting up NGINX Plus Dashboard, active health checks and view the metrics.
2. Configuring key-value store and enable IP allow/deny list.
3. Configuring Cache Manager.
4. Enabling JWT Authentication.
5. NGINX HA mode, Sync configuration and State Sharing Cluster (Option).
6. Summary and Q&A.

## เตรียมตัวก่อนการทดสอบ
1. ติดตั้ง Ubuntu 18.04 Local VM หรือ Cloud Instance

- ทำการ Copy โฟรเดอร์ Apps (App1, App2, App3, covid-app & jwt-app) ไปไว้ที่ภายใต้ "/opt/services"
- กำหนดไฟล์ hosts บนเครื่อง <br>
 ``<internal-ip> example.com www.example.com example123.com www.example123.com ``

2. ติดตั้ง NGINX Plus (Lasted version).
-  NGINX Plus Trial License ได้จาก https://www.nginx.com/free-trial-request


##  1. Live Activity Dashboard.
อ้างอิงไฟล์  [dashboard.conf](dashboard.conf)
- ในไฟล์ .conf มี servers อยู่ 3 Apps ให้บริการที่พอร์ต`` 9001, 9002`` และ ``9003.``
- Load Balancing ถูกตั้งค่า และเปิดบริการที่พอร์ต ``9000``.
- API / Dashboard ให้บริการที่พอร์ต ``8080``.
    - http://ip-address:8080
    - http://ip-address:8080/swagger-ui/

#### ตัวอย่างและข้อมูลเพิ่มเติม :
* [Live Activity Monitoring with N+](https://docs.nginx.com/nginx/admin-guide/monitoring/live-activity-monitoring/)
* [Stub Status Module for NGINX](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html)
* [Prometheus Exporter](https://github.com/nginxinc/nginx-prometheus-exporter)

##  2. Key-Value Store.
อ้างอิงไฟล์ [key.value.store.conf](key.value.store.conf)
### 2.1 IP Allow/Deny List
```
$ curl -s -X GET 'http://<ip-address>:8080/api/6/http/keyvals/allowlist_zone' | jq

$ curl -X POST -d '{"<internal-ip>":"1"}' -s 'http://ip-address:8080/api/6/http/keyvals/allowlist_zone'

$ curl -X PATCH -d '{"<internal-ip>":"0"}' -s 'http://ip-address:8080/api/6/http/keyvals/allowlist_zone'

$ curl -s -X DELETE 'http://<ip-address>:8080/api/6/http/keyvals/allowlist_zone'
```
- ทำการ blocked access สำหรับ internal IP. ค่า `1` ให้ Deny และ `0`  ให้ Allow.


### 2.2 SSL Certificate Management
อ้างอิงไฟล์ [key.value.store.conf](key.value.store.conf)
#### ตัวอย่างและข้อมูลเพิ่มเติม :
* [SSL Termination](https://docs.nginx.com/nginx/admin-guide/security-controls/terminating-ssl-http/)
* [Dynamic SSL Key Management: YouTube](https://www.youtube.com/watch?v=aeLE988jmlo&ab_channel=NGINX%2CInc)
* [Dynamic SSL Key Management: GitHub](https://github.com/jay-nginx/dynamic-ssl-management)
* [$ssl_server_name - Variable](http://nginx.org/en/docs/http/ngx_http_ssl_module.html#var_ssl_server_name)


## 3. Cache Management.
อ้างอิงไฟล์ [cache.management.conf](cache.management.conf)

#### ตัวอย่างและข้อมูลเพิ่มเติม :
* [Content Caching](https://docs.nginx.com/nginx/admin-guide/content-cache/content-caching/)
* [A Detailed Guide to Caching: Blog](https://www.nginx.com/blog/nginx-caching-guide/)
* [proxy_cache - Directive](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_cache)

## 4. JWT Validation.
อ้างอิงไฟล์  [jwt.validation.conf](jwt.validation.conf)

#### ตัวอย่างและข้อมูลเพิ่มเติม :
* [NGINX Demo A/B Testing with JWT Routing](https://jaturaprom.medium.com/nginx-demo-demo-4-a-b-testing-with-jwt-9e132af4845)
* [JWTs for Authentication and Content Based Routing](https://www.nginx.com/blog/authentication-content-based-routing-jwts-nginx-plus/)
* [Setting up JWT: Tech Doco](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-jwt-authentication/)
* [auth_jwt - Directive](http://nginx.org/en/docs/http/ngx_http_auth_jwt_module.html)

## 5. NGINX HA.
### 5.1 NGINX Plus HA modes (Active-Standby/Active-Active).
- https://docs.nginx.com/nginx/admin-guide/high-availability
### 5.2 NGINX Plus Synchronizing Configuration in Cluster. 
- https://docs.nginx.com/nginx/admin-guide/high-availability/configuration-sharing
### 5.3 NGINX Plus State Sharing in Cluster.
อ้างอิงโฟเดอร์ [zone-sync-example](zone-sync-example)
- https://docs.nginx.com/nginx/admin-guide/high-availability/zone_sync

## Closing Credits.
 ####  Credit by 
 - **[Jay Desai](https://github.com/jay-nginx)**

 #### Update and moddify by
- **[Supachai-j](https://github.com/supachai-j)**