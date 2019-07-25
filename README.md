# Deploy Drone CI
[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors-)

[![Stack](https://raw.githubusercontent.com/paralect/stack/master/stack-component-template/stack.png)](https://github.com/paralect/stack)

[![All Contributors](https://img.shields.io/badge/all_contributors-3-orange.svg?style=flat-square)](#contributors)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Build Status](http://product-stack-ci.paralect.com/api/badges/paralect/deploy-drone/status.svg)](http://product-stack-ci.paralect.com/paralect/deploy-drone)
[![David Dependancy Status](https://david-dm.org/paralect/deploy-drone.svg)](https://david-dm.org/paralect/deploy-drone)

[![Watch on GitHub](https://img.shields.io/github/watchers/paralect/deploy-drone.svg?style=social&label=Watch)](https://github.com/paralect/deploy-drone/watchers)
[![Star on GitHub](https://img.shields.io/github/stars/paralect/deploy-drone.svg?style=social&label=Stars)](https://github.com/paralect/deploy-drone/stargazers)
[![Follow](https://img.shields.io/twitter/follow/paralect.svg?style=social&label=Follow)](https://twitter.com/paralect)
[![Tweet](https://img.shields.io/twitter/url/https/github.com/paralect/ship.svg?style=social)](https://twitter.com/intent/tweet?text=I%27m%20building%20my%20next%20product%20with%20Ship%20%F0%9F%9A%80.%20Check%20it%20out:%20https://github.com/paralect/ship)


Prerequisites:

1. [Ansible](http://docs.ansible.com/ansible/intro_installation.html)
2. Ubuntu 16.04 server & ssh access to that server

Installation steps:

1. Update server ip in `hosts` file. If you are planning to use same server for both drone and nginx - just put same ip for both, drone & nginx targets.
2. Install Ansible role dependencies with one command: `./bin/install-ansible-dependencies.sh`
3. Update github application callback url to either point to your server ip address or your domain. For example:
`http://ci.myapp.com/login` or just `http://server_ip/login`.
4. Set server ip variable or domain name in `vars/main.yml` (`nginx_drone_server_name` variable).
5. Update `drone_user_create` in `vars/main.yml` - github user, who will be initial administrator and will be able to grant the administrator role to additional accounts.
6. Rename `credentials-template.yml` into `credentials.yml` and update your github clientId, clientSecret as well as username and password for PostgreSQL database.

Once you done all above, run the following command:

```
./bin/setup-server.sh && ./bin/deploy-drone.sh
```

You should have Drone CI installed by now. The only step remaining is to make Drone work behind Nginx proxy.

### Setting up Nginx for Drone CI

If you would like to install nginx on a same server with Drone CI - just run following command:

```
./bin/setup-nginx.sh
```

If you already have nginx installed somewhere else and just would like to attach drone nginx configuration to existing nginx server you can do following:

1. Set nginx server ip in `hosts` file for the nginx target
2. Run same command `./bin/setup-nginx.sh`, but reply `no` to the question about nginx installation.

In this case nginx configuration for Drone CI will be copied to the existing nginx server.


### Setting up ssl for production Drone CI

1. Place your ssl keys into int ssl-keys directory as app.crt and app.key (they are in a `.gitignore`)
2. Make sure that `server_setup_ssl` is set to true in `vars/main.yml`
3. Deploy ssl using `./bin/setup-server.sh --tags "nginx"`
4. Update callback url in the Github application to start from `https`

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/Mar1nka"><img src="https://avatars1.githubusercontent.com/u/25400321?v=4" width="100px;" alt="Mar1nka"/><br /><sub><b>Mar1nka</b></sub></a><br /><a href="https://github.com/paralect/deploy-drone/commits?author=Mar1nka" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
