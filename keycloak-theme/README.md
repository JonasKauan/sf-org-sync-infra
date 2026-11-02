# Tema de login do Keycloak

O tema `sf-org-manager` usa os templates HTML/FreeMarker oficiais do Keycloak 26.8.1 e aplica o visual da tela de login do frontend: fundo azul claro, cartão branco, tipografia escura e botões azuis. Os formulários de login, recuperação de senha, cadastro, OTP e mensagens continuam sob controle do Keycloak.

## Instalação no Keycloak

O `docker-compose-dev.yaml` monta este tema em `/opt/keycloak/themes/sf-org-manager` no container. Para iniciar o Keycloak a partir da raiz deste repositório:

```sh
docker compose --env-file .env.dev -f docker-compose-dev.yaml up -d keycloak
```

Em outro Docker Compose, monte a pasta do tema com um caminho relativo ao arquivo Compose:

```yaml
services:
  keycloak:
    volumes:
      - ./keycloak-theme/sf-org-manager:/opt/keycloak/themes/sf-org-manager:ro
```

Depois de iniciar/reiniciar o container, acesse `http://localhost:8180/auth/admin/`. No Admin Console do realm desejado, abra **Realm settings → Themes**, escolha `sf-org-manager` em **Login theme** e salve. Em **Realm settings → General**, defina **Display name** como `SF Org Manager` para mostrar o nome do app acima do cartão. Para exibir os textos em português, habilite **Internationalization** em **Realm settings → Localization** e defina `Português (Brasil)` como idioma padrão.

O tema precisa ser servido pelo Keycloak; os arquivos nesta pasta não entram no build do Vite. Para ajustar CSS durante o desenvolvimento, desabilite temporariamente o cache de temas do Keycloak com `--spi-theme--static-max-age=-1 --spi-theme--cache-themes=false --spi-theme--cache-templates=false`. Reative o cache no ambiente final.
