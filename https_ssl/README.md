# HTTPS SSL

DNS subdomain auditing script and HAProxy SSL termination and HTTP-to-HTTPS redirect configurations for `mutabazi.tech` (`7113-web-01` at `13.40.85.82`, `7113-web-02` at `35.179.127.188`, and `7113-lb-01` at `16.60.113.174`).

## Files

* `0-world_wide_web`: Bash script using a function and `awk` to query DNS records via `dig` and print `The subdomain [SUB_DOMAIN] is a [RECORD_TYPE] record and points to [DESTINATION]` for `www`, `lb-01`, `web-01`, and `web-02` (or a single specified subdomain).
* `1-haproxy_ssl_termination`: HAProxy configuration (`/etc/haproxy/haproxy.cfg`) terminating SSL on TCP port `443` for `www.mutabazi.tech` and forwarding traffic to `7113-web-01` and `7113-web-02`.
* `2-redirect_http_to_https`: HAProxy configuration (`/etc/haproxy/haproxy.cfg`) redirecting HTTP (`:80`) traffic to HTTPS (`:443`) with a `301` status while serving SSL on `:443`.

## Usage

```bash
./0-world_wide_web mutabazi.tech
./0-world_wide_web mutabazi.tech web-02
```
