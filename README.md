# Sonata demo aplikace

## Postup instalace

#### 1. naklonujeme repozitář např. do www složky

    git clone https://github.com/rapemer/SonataDemoBundle.git sonata-demo
    cd sonata-demo

#### 2. instalace závislostí přes composer

    composer install

#### 3. konfigurace parametrů `app/config/parameters.yml`

Na konci Vás instalátor provede nastavením databáze a dalších parametrů. Než dokončíte nastavení těchto parametrů, vytvořte ručně databázi (např. pomocí Admineru, PhpMyAdmin nebo z konzole). Jinak dojde na konci instalace k chybě: `SQLSTATE[HY000] [1049] Unknown database 'sonata-demo'`. 

Pro fajnšmejkry lze samozřejmě vytvořit composer post-script, který po konfiguraci parametrů spustí příkaz `php app/console doctrine:database:create`, ale prozatím databázi vytvoříme ručně.

### Po úspěšném dokončení `composer install` pokračujeme příkazy:

#### 4. update databázového schéma

Dump, který nám zobrazí SQL příkazy, které chceme nad databází vykonat:

    php app/console doctrine:schema:update --dump-sql

SQL můžeme zkopírovat a spustit ručně nebo spustíme příkaz s parametrem --force:

    php app/console doctrine:schema:update --force

Čímž updatujeme databázové schéma ihned a ušetříme si pracnost s ruční prací.

#### 5. Instalace stylů, javascriptů apod.:

    php app/console assets:install

Příkaz nainstaluje veškeré soubory z každého bundlu (umístěno uvnitř složky `[BundleName]/Resources/public/*`) do složky `web/bundles/[bundlename]/*`

Na Windows se soubory kopírují. Na Linuxu můžete přidat parametr `php app/console assets:install --symlink`, čímž vytvoříte pouze symbolické odkazy a nedochází tak ke kopírování souborů.

Ze srandy můžete tento příkaz spustit jako `php app/console ass:in`. Jedná se o přezdívku, která funguje s jakýmkoli jiným Symfony Commandem. Příkaz `php app/console doctrine:generate:entity` tak můžeme zapsat třeba jen jako `php app/console do:ge:entity`. Symfony si automaticky doplní názvy a rozpozná, který příkaz chcete spustit. Pokud je více shod, informuje Vás o tom chybovou hláškou a požádá Vás o upřesnění příkazu. Například `doctrine:generate:entities` a `doctrine:generate:entity` nelze identifikovat pomocí `do:ge:en`. 

#### 6. Vytvoření uživatele administrace (vyplníte uživatelské jméno, email a heslo):

Vytvoření hlavního administrátora:

    php app/console fos:user:create --super-admin

Při vyplňování hesla dávejte pozor, bude viditelné na obrazovce terminálu.

#### 7. Spuštění zabudovaného Symfony serveru (pokud nechcete konfigurovat Apache):

    php app/console server:run

Následně máme k dispozici URL adresu [localhost:8000/admin](http://localhost:8000/admin), kde si můžeme zobrazit administraci a přihlásit se pomocí uživatele vytvořeného v kroku 6.

Touto adresou prohlížíme tzv. `prod` prostředí Symfony aplikace. Chceme-li si zobrazit `dev` prostředí (kde najdete užitečný profiler), použijeme adresu [localhost:8000/app_dev.php/admin](http://localhost:8000/app_dev.php/admin). Více o Symfony prostředí se dočtete v [oficiální dokumentaci](http://symfony.com/doc/current/cookbook/configuration/environments.html#different-environments-different-configuration-files).

### Příjemnou zábavu se Sonatou
