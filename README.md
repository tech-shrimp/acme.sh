# An ACME Shell script: acme.sh 

- An ACME protocol client written purely in Shell (Unix shell) language.
- Full ACME protocol implementation.
- Support ECDSA certs
- Support SAN and wildcard certs
- Simple, powerful and very easy to use. You only need 3 minutes to learn it.
# 1. How to install
```bash
curl https://get.acme.sh | sh -s email=my@example.com
```
# 2. Just issue a cert
```bash
acme.sh --issue -d example.com -w /home/wwwroot/example.com
```
# 3. Install the cert to Apache/Nginx etc.
**Nginx** example:
```bash
acme.sh --install-cert -d example.com \
--key-file       /path/to/keyfile/in/nginx/key.pem  \
--fullchain-file /path/to/fullchain/nginx/cert.pem \
--reloadcmd     "service nginx force-reload"
```

# 8. Automatic DNS API integration

If your DNS provider supports API access, we can use that API to automatically issue the certs.

You don't have to do anything manually!

### Currently acme.sh supports most of the dns providers:

https://github.com/acmesh-official/acme.sh/wiki/dnsapi

# 9. Use DNS manual mode:

See: https://github.com/acmesh-official/acme.sh/wiki/dns-manual-mode first.

If your dns provider doesn't support any api access, you can add the txt record by hand.

```bash
acme.sh --issue --dns -d example.com -d www.example.com -d cp.example.com
```

You should get an output like below:

```sh
Add the following txt record:
Domain:_acme-challenge.example.com
Txt value:9ihDbjYfTExAYeDs4DBUeuTo18KBzwvTEjUnSwd32-c

Add the following txt record:
Domain:_acme-challenge.www.example.com
Txt value:9ihDbjxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

Please add those txt records to the domains. Waiting for the dns to take effect.
```

Then just rerun with `renew` argument:

```bash
acme.sh --renew -d example.com
```

Ok, it's done.

**Take care, this is dns manual mode, it can not be renewed automatically. you will have to add a new txt record to your domain by your hand when you renew your cert.**

**Please use dns api mode instead.**

# 10. Issue ECC certificates

Just set the `keylength` parameter with a prefix `ec-`.

For example:

### Single domain ECC certificate

```bash
acme.sh --issue -w /home/wwwroot/example.com -d example.com --keylength ec-256
```

### SAN multi domain ECC certificate

```bash
acme.sh --issue -w /home/wwwroot/example.com -d example.com -d www.example.com --keylength ec-256
```

Please look at the `keylength` parameter above.

Valid values are:

1. **ec-256 (prime256v1, "ECDSA P-256", which is the default key type)**
2. **ec-384 (secp384r1,  "ECDSA P-384")**
3. **ec-521 (secp521r1,  "ECDSA P-521", which is not supported by Let's Encrypt yet.)**
4. **2048   (RSA2048)**
5. **3072   (RSA3072)**
6. **4096   (RSA4096)**


# 11. Issue Wildcard certificates

It's simple, just give a wildcard domain as the `-d` parameter.

```sh
acme.sh  --issue -d example.com  -d '*.example.com'  --dns dns_cf
```



# 12. How to renew the certs

No, you don't need to renew the certs manually. All the certs will be renewed automatically every **60** days.

However, you can also force to renew a cert:

```sh
acme.sh --renew -d example.com --force
```

or, for ECC cert:

```sh
acme.sh --renew -d example.com --force --ecc
```


# 13. How to stop cert renewal

To stop renewal of a cert, you can execute the following to remove the cert from the renewal list:

```sh
acme.sh --remove -d example.com [--ecc]
```

The cert/key file is not removed from the disk.

You can remove the respective directory (e.g. `~/.acme.sh/example.com`) by yourself.


# 14. How to upgrade `acme.sh`

acme.sh is in constant development, so it's strongly recommended to use the latest code.

You can update acme.sh to the latest code:

```sh
acme.sh --upgrade
```

You can also enable auto upgrade:

```sh
acme.sh --upgrade --auto-upgrade
```

Then **acme.sh** will be kept up to date automatically.

Disable auto upgrade:

```sh
acme.sh --upgrade --auto-upgrade 0
```


# 15. Issue a cert from an existing CSR

https://github.com/acmesh-official/acme.sh/wiki/Issue-a-cert-from-existing-CSR


# 16. Send notifications in cronjob

https://github.com/acmesh-official/acme.sh/wiki/notify


# 17. Under the Hood

Speak ACME language using shell, directly to "Let's Encrypt".

TODO:


# 18. Acknowledgments

1. Acme-tiny: https://github.com/diafygi/acme-tiny
2. ACME protocol: https://github.com/ietf-wg-acme/acme


## Contributors

### Code Contributors

This project exists thanks to all the people who contribute.
<a href="https://github.com/acmesh-official/acme.sh/graphs/contributors"><img src="https://opencollective.com/acmesh/contributors.svg?width=890&button=false" /></a>

### Financial Contributors

Become a financial contributor and help us sustain our community. [[Contribute](https://opencollective.com/acmesh/contribute)]

#### Individuals

<a href="https://opencollective.com/acmesh"><img src="https://opencollective.com/acmesh/individuals.svg?width=890"></a>

#### Organizations

Support this project with your organization. Your logo will show up here with a link to your website. [[Contribute](https://opencollective.com/acmesh/contribute)]

<a href="https://opencollective.com/acmesh/organization/0/website"><img src="https://opencollective.com/acmesh/organization/0/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/1/website"><img src="https://opencollective.com/acmesh/organization/1/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/2/website"><img src="https://opencollective.com/acmesh/organization/2/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/3/website"><img src="https://opencollective.com/acmesh/organization/3/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/4/website"><img src="https://opencollective.com/acmesh/organization/4/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/5/website"><img src="https://opencollective.com/acmesh/organization/5/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/6/website"><img src="https://opencollective.com/acmesh/organization/6/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/7/website"><img src="https://opencollective.com/acmesh/organization/7/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/8/website"><img src="https://opencollective.com/acmesh/organization/8/avatar.svg"></a>
<a href="https://opencollective.com/acmesh/organization/9/website"><img src="https://opencollective.com/acmesh/organization/9/avatar.svg"></a>



# 19. License & Others

License is GPLv3

Please Star and Fork me.

[Issues](https://github.com/acmesh-official/acme.sh/issues) and [pull requests](https://github.com/acmesh-official/acme.sh/pulls) are welcome.


# 20. Donate
Your donation makes **acme.sh** better:

1. PayPal/Alipay(支付宝)/Wechat(微信): [https://donate.acme.sh/](https://donate.acme.sh/)

[Donate List](https://github.com/acmesh-official/acme.sh/wiki/Donate-list)
