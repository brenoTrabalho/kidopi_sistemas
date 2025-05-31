# Kidopi Sistemas

	Ambiente de desenvolvimento para sistemas PHP 5.6, MySQL e MongoDB utilizando Docker.

## Pré-requisitos

	- [Docker](https://docs.docker.com/get-docker/)
	- [Docker Compose](https://docs.docker.com/compose/)

## Passos para iniciar o projeto

	1. **Clone este repositório**
		```bash
			git clone git@github.com:brenoTrabalho/kidopi_sistemas.git
			cd seu-repositorio/kidopi_sistemas
		```

	2. **Crie as pastas necessárias**
		> Essas pastas são ignoradas pelo Git e devem ser criadas localmente:
		```bash
			mkdir -p documentos/kidopi_testes dump logs mongo www/CleverCare www/saudecorp www/gplc
		```

	3. **Crie o arquivo `.env`**
		Peça o arquivo .env a eu, breno o criador

	4. **Clone os repositórios necessários**
	
		```bash
			# saudecorp:
				git clone git@bitbucket.org:kidopi/saudecorp.git www/saudecorp
			# CleverCare:
				git clone git@bitbucket.org:kidopi/clevercare_git.git www/CleverCare
			# gplc:
				git clone git@bitbucket.org:kidopi/gplc_git.git www/gplc
		```

	5. **Suba o ambiente com Docker Compose**
		```bash
   			docker compose up -d
   		```

	6. **Acesse os serviços**
		- **Aplicação PHP:** [http://localhost:80](http://localhost:80)
		- **phpMyAdmin:** [http://localhost:8081](http://localhost:8081)
		- **MySQL:** porta definida em `MYSQL_PORT`
		- **MongoDB:** porta definida em `MONGO_PORT`

### Exemplo: Importar banco MySQL

	Coloque o arquivo `CleverCareDump.sql` na pasta `dump` e execute:

	```bash
		docker exec -i mysql mysql -u root -p"$MYSQL_ROOT_PASSWORD" "kidopi_care" < dump/CleverCareDump.sql
	```
## Observações

	- Os arquivos de log são gerados automaticamente nas pastas ignoradas.
	- O arquivo `.env` **não** é versionado, crie o seu localmente.
	- As pastas `kidopi_testes`, `dump`, `logs`, `mongo`, `CleverCare`, `saudecorp` e `gplc` são ignoradas pelo Git.

---