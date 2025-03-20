# PostgreSQL container image with pgvector for Bitnami PostgreSQL Helm Chart 🐘

The PostgreSQL container image includes pgvector. By using this image, you can deploy PostgreSQL with pgvector to Kubernetes using [Bitnami PostgreSQL Helm Chart](https://github.com/bitnami/charts/tree/main/bitnami/postgresql).

## Note

- For testing purposes only. Not for production.

## Usage

1. Set image configurations in your custom values file for example `postgresql.yaml`. You can see the sample values file [here](./sample/postgresql.yaml).

   ```yaml
   global:
     security:
       allowInsecureImages: true

   image:
     registry: "ghcr.io"
     repository: "kota2and3kan/bitnami-postgresql-pgvector"
     tag: "17"
   ```
   - Note: You can see the list of tag in [Versions page of GitHub Packages](https://github.com/users/kota2and3kan/packages/container/bitnami-postgresql-pgvector/versions?filters%5Bversion_type%5D=tagged).

1. Deploy PostgreSQL with pgvector.

   ```console
   helm install postgresql-pgvector \
     --set auth.postgresPassword=postgres \
     --values postgresql.yaml \
     oci://registry-1.docker.io/bitnamicharts/postgresql
   ```

1. Enable pgvector in PostgreSQL.

   ```console
   kubectl exec -it postgresql-pgvector-0 -- psql -U postgres -c 'CREATE EXTENSION IF NOT EXISTS vector' -c '\dx'
   ```
   - Note: You must enter the password of `postgres` user that you specified to the `--set auth.postgresPassword=********` option in the previous step.
