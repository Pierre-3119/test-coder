FROM mcr.microsoft.com/devcontainers/dotnet:1-8.0

# Remove the yarn repository to avoid expired Yarn GPG key issues
# See : https://github.com/alshedivat/al-folio/issues/3487
RUN rm -f /etc/apt/sources.list.d/yarn.list

# Add postgresql-client for direct database access via psql
RUN apt-get update && apt-get install -y postgresql-client

# Add ldap-utils for direct LDAP access via ldapsearch
RUN apt-get update && apt-get install -y ldap-utils