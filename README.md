# Desafio-contar-palavras-do-livro-sherlock-com-ecossistema-na-AWS
Desafio do curso Criando seu Ecossistema de Big Data na Nuvem proposto pela DIO

Passos realizados para conclusão do desafio: 

1.	Acesso ao console da AWS para criação do Bucket "dio-live-datalake-prodel" no S3;
2.	Dentro do Bucket foi criada uma estrutura de pastas com os seguintes nomes: data, output e temp;
3.	Acesso ao EC2 através do console para criação do par de chaves. As chaves foram criadas no formato "pem". O Download das chaves foi feito automaticamente pelo console;
4.	Acesso ao "Security Credentials" para criação da chave de acesso. A chave foi criada e em seguida realizado o download do arquivo csv;
5.	No linux (WSL), foi criado um ambiente virtual com o seguinte comando: virtualenv --python=python3.6 venv_diolive_prod;
6.	Foi startado o ambiente virtual python com o comando: source venv_diolive_prod/bin/activate;
7.	De volta ao S3 foi realizado o upload (via console) do arquivo "sherlock.txt" para dentro do diretório "data" contido no Bucket "dio-live-datalake-prodel";
8.	No ambiente linux, foi necessário editar o arquivo mrjob.conf através do editor de textos "nano", para acrescentar as informações das chaves secretas (access key id, crecret access key, key pair, e key pair file);
9.	Foi necessário instalar o serviço de SSH no ambiente linux (comando sudo apt install ssh);
10.	Com o mrjob.conf configurado, foi necessário copiar o conteúdo do arquivo .pem baixado do AWS para o arquivo .pem indicado no mrjob.conf (dio-live-key-prod.pem);
11.	O próximo passo foi instalar as bibliotecas "boto3" e "mrjob" com os comandos: "pip install boto3" e "pip install mrjob";
12.	Em seguida, foi executado o comando para startar o algoritmo Python (dio-live-wordcount-test.py) para iniciar o JOB.  O comando utilizado foi: 

python3 dio-live-wordcount-test.py -r emr s3://dio-live-datalake-prodel/data/sherlock.txt --output-dir=s3://dio-live-datalake-prodel/output/logs1 --cloud-tmp-dir=s3://dio-live-datalake-prodel/temp/

13.	Com o comando concluído, foram gerados 5 arquivos no diretório output/logs-01 (part-00000, part-00001, part-00002, part-00003 e part-00004), além de um arquivo _SUCCESS. Assim concluindo o desafio.
