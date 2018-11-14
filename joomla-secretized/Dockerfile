FROM "joomla:3.9-apache"

COPY "./env_secrets_expand.sh" "/"

ENTRYPOINT ["/env_secrets_expand.sh", "/entrypoint.sh"]
CMD ["apache2-foreground"]
