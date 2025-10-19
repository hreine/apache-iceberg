
Esta guía le ayudará a empezar a usar Apache Iceberg™ con Apache Spark™, ​​e incluye código de ejemplo para destacar algunas funciones potentes. Puede obtener más información sobre el entorno de ejecución Spark de Iceberg consultando la sección de Spark.

Docker-Compose:

La forma más rápida de empezar es usar un archivo docker-compose que use la imagen tabulario/spark-iceberg, la cual contiene un clúster local de Spark con un catálogo de Iceberg configurado. Para usarlo, necesitará instalar la CLI de Docker y la CLI de Docker Compose.

Una vez que las tenga, guarde el archivo .yaml a continuación en un archivo llamado docker-compose.yml:

```
services:
  spark-iceberg:
    image: tabulario/spark-iceberg
    container_name: spark-iceberg
    build: spark/
    networks:
      iceberg_net:
    depends_on:
      - rest
      - minio
    volumes:
      - ./warehouse:/home/iceberg/warehouse
      - ./notebooks:/home/iceberg/notebooks/notebooks
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
    ports:
      - 8888:8888
      - 8080:8080
      - 10000:10000
      - 10001:10001
  rest:
    image: apache/iceberg-rest-fixture
    container_name: iceberg-rest
    networks:
      iceberg_net:
    ports:
      - 8181:8181
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
      - CATALOG_WAREHOUSE=s3://warehouse/
      - CATALOG_IO__IMPL=org.apache.iceberg.aws.s3.S3FileIO
      - CATALOG_S3_ENDPOINT=http://minio:9000
  minio:
    image: minio/minio
    container_name: minio
    environment:
      - MINIO_ROOT_USER=admin
      - MINIO_ROOT_PASSWORD=password
      - MINIO_DOMAIN=minio
    networks:
      iceberg_net:
        aliases:
          - warehouse.minio
    ports:
      - 9001:9001
      - 9000:9000
    command: ["server", "/data", "--console-address", ":9001"]
  mc:
    depends_on:
      - minio
    image: minio/mc
    container_name: mc
    networks:
      iceberg_net:
    environment:
      - AWS_ACCESS_KEY_ID=admin
      - AWS_SECRET_ACCESS_KEY=password
      - AWS_REGION=us-east-1
    entrypoint: |
      /bin/sh -c "
      until (/usr/bin/mc alias set minio http://minio:9000 admin password) do echo '...waiting...' && sleep 1; done;
      /usr/bin/mc rm -r --force minio/warehouse;
      /usr/bin/mc mb minio/warehouse;
      /usr/bin/mc policy set public minio/warehouse;
      tail -f /dev/null
      "
networks:
  iceberg_net:
```


Inicie los contenedores Docker con este comando:

´´´
docker-compose up
´´´

You can then run any of the following commands to start a Spark session.

SparkSQL: ´docker exec -it spark-iceberg spark-sql´

SparkShell: ´docker exec -it spark-iceberg spark-shell´

pySpark: ´docker exec -it spark-iceberg pyspark´


Puede abrir el servidor de jupyter en http://localhost:8888


 CREATE NAMESPACE demo.nyc;

 docker exec spark-iceberg spark-submit "/home/iceberg/notebooks/notebooks/pipeline.py"