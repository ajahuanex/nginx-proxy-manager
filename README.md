<p align="center">
	<img src="https://nginxproxymanager.com/github.png">
	<br><br>
	<img src="https://img.shields.io/badge/version-2.9.9-green.svg?style=for-the-badge">
	<a href="https://hub.docker.com/repository/docker/jc21/nginx-proxy-manager">
		<img src="https://img.shields.io/docker/stars/jc21/nginx-proxy-manager.svg?style=for-the-badge">
	</a>
	<a href="https://hub.docker.com/repository/docker/jc21/nginx-proxy-manager">
		<img src="https://img.shields.io/docker/pulls/jc21/nginx-proxy-manager.svg?style=for-the-badge">
	</a>
	<a href="https://ci.nginxproxymanager.com/blue/organizations/jenkins/nginx-proxy-manager/branches/">
		<img src="https://img.shields.io/jenkins/build?jobUrl=https%3A%2F%2Fci.nginxproxymanager.com%2Fjob%2Fnginx-proxy-manager%2Fjob%2Fmaster&style=for-the-badge">
	</a>
	<a href="https://gitter.im/nginx-proxy-manager/community">
		<img alt="Gitter" src="https://img.shields.io/gitter/room/nginx-proxy-manager/community?style=for-the-badge">
	</a>
	<a href="https://reddit.com/r/nginxproxymanager">
		<img alt="Reddit" src="https://img.shields.io/reddit/subreddit-subscribers/nginxproxymanager?label=Reddit%20Community&style=for-the-badge">
	</a>
</p>
Este proyecto viene como una imagen docker prediseñada, que le permite reenviar fácilmente a sus sitios web que se ejecutan en modo local o de otro modo, incluido SSL gratuito, sin tener que saber demasiado sobre Nginx o Letsencrypt.

- [Quick Setup](#quick-setup)
- [Full Setup](https://nginxproxymanager.com/setup/)
- [Screenshots](https://nginxproxymanager.com/screenshots/)

## Objetivo del proyecto

Se creó este proyecto para satisfacer una necesidad personal de proporcionar a los usuarios una manera fácil de lograr hosts de proxy inverso con terminación SSL y tenía que ser tan fácil que un mono pudiera hacerlo. Este objetivo no ha cambiado. Si bien puede haber opciones avanzadas, son opcionales y el proyecto debe ser lo más simple posible para que la barrera de entrada aquí sea baja.


<a href="https://www.buymeacoffee.com/jc21" target="_blank"><img src="http://public.jc21.com/github/by-me-a-coffee.png" alt="Buy Me A Coffee" style="height: 51px !important;width: 217px !important;" ></a>


## Características

- Interfaz de administración hermosa y segura basada en [Tabler](https://tabler.github.io/)
- Cree fácilmente dominios de reenvío, redirecciones, transmisiones y hosts 404 sin saber nada sobre Nginx
- SSL gratuito usando Let's Encrypt o proporcione sus propios certificados SSL personalizados
- Listas de acceso y autenticación HTTP básica para sus hosts
- Configuración avanzada de Nginx disponible para superusuarios
- Gestión de usuarios, permisos y registro de auditoría


## Hosting para su red local


No entraré en demasiados detalles aquí, pero aquí están los conceptos básicos para alguien nuevo en este mundo autohospedado.

1. El enrutador local tendrá una sección de reenvío de puertos en algún lugar. Inicie sesión y encuéntrelo
2. Agregue el reenvío de puertos para los puertos 80 y 443 al servidor que aloja este proyecto
3. Configure los detalles de su nombre de dominio para que apunten a servidor, ya sea con una IP estática o un servicio como DuckDNS o [Amazon Route53](https://github.com/jc21/route53-ddns)
4. Utilice Nginx Proxy Manager como su puerta de enlace para reenviar a sus otros servicios basados en web

## Configuración rápida

1. Instalar Docker y Docker-Compose

- [Documentación de instalación de Docker](https://docs.docker.com/install/)
- [Documentación de instalación de Docker-Compose](https://docs.docker.com/compose/install/)

2. Cree un archivo docker-compose.yml similar a este:

```yml
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "npm"
      DB_MYSQL_PASSWORD: "npm"
      DB_MYSQL_NAME: "npm"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
  db:
    image: 'jc21/mariadb-aria:latest'
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npm'
    volumes:
      - ./data/mysql:/var/lib/mysql
```

3. Trae tu stack(pila)

```bash
docker-compose up -d
```

4. Ingicie sesión en la interfaz de usuario Admin

Cuando su contenedor docker se esté ejecutando, conéctese a él en el puerto `81` para la interfaz de administración.
A veces, esto puede tardar un poco debido a la entropía de las claves.

[http://127.0.0.1:81](http://127.0.0.1:81)

Default Admin User:
```
Email:   admin@example.com
Password: changeme
```

Inmediatamente después de iniciar sesión con este usuario predeterminado, se le pedirá que modifique sus datos y cambie su contraseña.

## Colaboradores

Un agradecimiento especial a los siguientes colaboradores:

<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
	<tr>
		<td align="center">
			<a href="https://github.com/Subv">
				<img src="https://avatars1.githubusercontent.com/u/357072?s=460&u=d8adcdc91d749ae53e177973ed9b6bb6c4c894a3&v=4" width="80" alt=""/>
				<br /><sub><b>Sebastian Valle</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Indemnity83">
				<img src="https://avatars3.githubusercontent.com/u/35218?s=460&u=7082004ff35138157c868d7d9c683ccebfce5968&v=4" width="80" alt=""/>
				<br /><sub><b>Kyle Klaus</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/theraw">
				<img src="https://avatars1.githubusercontent.com/u/32969774?s=460&u=6b359971e15685fb0359e6a8c065a399b40dc228&v=4" width="80" alt=""/>
				<br /><sub><b>ƬHE ЯAW</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/spalger">
				<img src="https://avatars2.githubusercontent.com/u/1329312?s=400&u=565223e38f1c052afb4c5dcca3fcf1c63ba17ae7&v=4" width="80" alt=""/>
				<br /><sub><b>Spencer</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Xantios">
				<img src="https://avatars3.githubusercontent.com/u/1507836?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Xantios Krugor</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/dpanesso">
				<img src="https://avatars2.githubusercontent.com/u/2687121?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>David Panesso</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/IronTooch">
				<img src="https://avatars3.githubusercontent.com/u/27360514?s=460&u=69bf854a6647c55725f62ecb8d39249c6c0b2602&v=4" width="80" alt=""/>
				<br /><sub><b>IronTooch</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/damianog">
				<img src="https://avatars1.githubusercontent.com/u/2786682?s=460&u=76c6136fae797abb76b951cd8a246dcaecaf21af&v=4" width="80" alt=""/>
				<br /><sub><b>Damiano</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/tfmm">
				<img src="https://avatars3.githubusercontent.com/u/6880538?s=460&u=ce0160821cc4aa802df8395200f2d4956a5bc541&v=4" width="80" alt=""/>
				<br /><sub><b>Russ</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/margaale">
				<img src="https://avatars3.githubusercontent.com/u/20794934?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Marcelo Castagna</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Steven-Harris">
				<img src="https://avatars2.githubusercontent.com/u/7720242?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Steven Harris</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/jlesage">
				<img src="https://avatars0.githubusercontent.com/u/1791123?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Jocelyn Le Sage</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/cmer">
				<img src="https://avatars0.githubusercontent.com/u/412?s=460&u=67dd8b2e3661bfd6f68ec1eaa5b9821bd8a321cd&v=4" width="80" alt=""/>
				<br /><sub><b>Carl Mercier</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/the1ts">
				<img src="https://avatars1.githubusercontent.com/u/84956?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Paul Mansfield</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/OhHeyAlan">
				<img src="https://avatars0.githubusercontent.com/u/11955126?s=460&u=fbaa5a1a4f73ef8960132c703349bfd037fe2630&v=4" width="80" alt=""/>
				<br /><sub><b>OhHeyAlan</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/dogmatic69">
				<img src="https://avatars2.githubusercontent.com/u/94674?s=460&u=ca7647de53145c6283b6373ade5dc94ba99347db&v=4" width="80" alt=""/>
				<br /><sub><b>Carl Sutton</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/tg44">
				<img src="https://avatars0.githubusercontent.com/u/31839?s=460&u=ad32f4cadfef5e5fb09cdfa4b7b7b36a99ba6811&v=4" width="80" alt=""/>
				<br /><sub><b>Gergő Törcsvári</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/vrenjith">
				<img src="https://avatars3.githubusercontent.com/u/2093241?s=460&u=96ce93a9bebabdd0a60a2dc96cd093a41d5edaba&v=4" width="80" alt=""/>
				<br /><sub><b>vrenjith</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/duhruh">
				<img src="https://avatars2.githubusercontent.com/u/1133969?s=460&u=c0691e6131ec6d516416c1c6fcedb5034f877bbe&v=4" width="80" alt=""/>
				<br /><sub><b>David Rivera</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/jipjan">
				<img src="https://avatars2.githubusercontent.com/u/1384618?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Jaap-Jan de Wit</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/jmwebslave">
				<img src="https://avatars2.githubusercontent.com/u/6118262?s=460&u=7db409c47135b1e141c366bbb03ed9fae6ac2638&v=4" width="80" alt=""/>
				<br /><sub><b>James Morgan</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/chaptergy">
				<img src="https://avatars2.githubusercontent.com/u/26956711?s=460&u=7d9adebabb6b4e7af7cb05d98d751087a372304b&v=4" width="80" alt=""/>
				<br /><sub><b>chaptergy</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Philip-Mooney">
				<img src="https://avatars0.githubusercontent.com/u/48624631?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Philip Mooney</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/WaterCalm">
				<img src="https://avatars1.githubusercontent.com/u/23502129?s=400&v=4" width="80" alt=""/>
				<br /><sub><b>WaterCalm</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/lebrou34">
				<img src="https://avatars1.githubusercontent.com/u/16373103?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>lebrou34</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/lightglitch">
				<img src="https://avatars0.githubusercontent.com/u/196953?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Mário Franco</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/klutchell">
				<img src="https://avatars3.githubusercontent.com/u/20458272?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Kyle Harding</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/ahgraber">
				<img src="https://avatars.githubusercontent.com/u/24922003?s=460&u=8376c9f00af9b6057ba4d2fb03b4f1b20a75277f&v=4" width="80" alt=""/>
				<br /><sub><b>Alex Graber</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/MooBaloo">
				<img src="https://avatars.githubusercontent.com/u/9493496?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>MooBaloo</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Shuro">
				<img src="https://avatars.githubusercontent.com/u/944030?s=460&v=4" width="80" alt=""/>
				<br /><sub><b>Shuro</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/lorisbergeron">
				<img src="https://avatars.githubusercontent.com/u/51918567?s=460&u=778e4ff284b7d7304450f98421c99f79298371fb&v=4" width="80" alt=""/>
				<br /><sub><b>Loris Bergeron</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/hepelayo">
				<img src="https://avatars.githubusercontent.com/u/8243119?v=4" width="80" alt=""/>
				<br /><sub><b>hepelayo</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/jonasled">
				<img src="https://avatars.githubusercontent.com/u/46790650?v=4" width="80" alt=""/>
				<br /><sub><b>Jonas Leder</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/stegmannb">
				<img src="https://avatars.githubusercontent.com/u/12850482?v=4" width="80" alt=""/>
				<br /><sub><b>Bastian Stegmann</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Stealthii">
				<img src="https://avatars.githubusercontent.com/u/998920?v=4" width="80" alt=""/>
				<br /><sub><b>Stealthii</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/thegamingninja">
				<img src="https://avatars.githubusercontent.com/u/8020534?v=4" width="80" alt=""/>
				<br /><sub><b>THEGamingninja</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/italobb">
				<img src="https://avatars.githubusercontent.com/u/1801687?v=4" width="80" alt=""/>
				<br /><sub><b>Italo Borssatto</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/GurjinderSingh">
				<img src="https://avatars.githubusercontent.com/u/3470709?v=4" width="80" alt=""/>
				<br /><sub><b>Gurjinder Singh</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/phantomski77">
				<img src="https://avatars.githubusercontent.com/u/69464125?v=4" width="80" alt=""/>
				<br /><sub><b>David Dosoudil</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/ijaron">
				<img src="https://avatars.githubusercontent.com/u/5156472?v=4" width="80" alt=""/>
				<br /><sub><b>ijaron</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/nielscil">
				<img src="https://avatars.githubusercontent.com/u/9073152?v=4" width="80" alt=""/>
				<br /><sub><b>Niels Bouma</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/ogarai">
				<img src="https://avatars.githubusercontent.com/u/2949572?v=4" width="80" alt=""/>
				<br /><sub><b>Orko Garai</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/baruffaldi">
				<img src="https://avatars.githubusercontent.com/u/36949?v=4" width="80" alt=""/>
				<br /><sub><b>Filippo Baruffaldi</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/bikram990">
				<img src="https://avatars.githubusercontent.com/u/6782131?v=4" width="80" alt=""/>
				<br /><sub><b>Bikramjeet Singh</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/razvanstoica89">
				<img src="https://avatars.githubusercontent.com/u/28236583?v=4" width="80" alt=""/>
				<br /><sub><b>Razvan Stoica</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/psharma04">
				<img src="https://avatars.githubusercontent.com/u/22587474?v=4" width="80" alt=""/>
				<br /><sub><b>RBXII3</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/demize">
				<img src="https://avatars.githubusercontent.com/u/264914?v=4" width="80" alt=""/>
				<br /><sub><b>demize</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/PUP-Loki">
				<img src="https://avatars.githubusercontent.com/u/75944209?v=4" width="80" alt=""/>
				<br /><sub><b>PUP-Loki</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/DSorlov">
				<img src="https://avatars.githubusercontent.com/u/8133650?v=4" width="80" alt=""/>
				<br /><sub><b>Daniel Sörlöv</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/Theyooo">
				<img src="https://avatars.githubusercontent.com/u/58510131?v=4" width="80" alt=""/>
				<br /><sub><b>Theyooo</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/mrdink">
				<img src="https://avatars.githubusercontent.com/u/514751?v=4" width="80" alt=""/>
				<br /><sub><b>Justin Peacock</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/ChrisTracy">
				<img src="https://avatars.githubusercontent.com/u/58871574?v=4" width="80" alt=""/>
				<br /><sub><b>Chris Tracy</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/Fuechslein">
				<img src="https://avatars.githubusercontent.com/u/15112818?v=4" width="80" alt=""/>
				<br /><sub><b>Fuechslein</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/nightah">
				<img src="https://avatars.githubusercontent.com/u/3339418?v=4" width="80" alt=""/>
				<br /><sub><b>Amir Zarrinkafsh</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/gabbe">
				<img src="https://avatars.githubusercontent.com/u/156397?v=4" width="80" alt=""/>
				<br /><sub><b>gabbe</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/bmbvenom">
				<img src="https://avatars.githubusercontent.com/u/20530371?v=4" width="80" alt=""/>
				<br /><sub><b>bmbvenom</b></sub>
			</a>
		</td>
	</tr>
	<tr>
		<td align="center">
			<a href="https://github.com/FMeinicke">
				<img src="https://avatars.githubusercontent.com/u/42121639?v=4" width="80" alt=""/>
				<br /><sub><b>Florian Meinicke</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/ssrahul96">
				<img src="https://avatars.githubusercontent.com/u/15570570?v=4" width="80" alt=""/>
				<br /><sub><b>Rahul Somasundaram</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/BjoernAkAManf">
				<img src="https://avatars.githubusercontent.com/u/833043?v=4" width="80" alt=""/>
				<br /><sub><b>Björn Heinrichs</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/realJoshByrnes">
				<img src="https://avatars.githubusercontent.com/u/204185?v=4" width="80" alt=""/>
				<br /><sub><b>Josh Byrnes</b></sub>
			</a>
		</td>
		<td align="center">
			<a href="https://github.com/bergi9">
				<img src="https://avatars.githubusercontent.com/u/5556750?v=4" width="80" alt=""/>
				<br /><sub><b>bergi9</b></sub>
			</a>
		</td>
	</tr>
</table>
<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
