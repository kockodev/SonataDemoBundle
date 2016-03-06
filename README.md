# Sonata demo aplikace

## Postup instalace

    git clone https://github.com/rapemer/SonataDemoBundle.git sonata-demo
    cd sonata-demo
    composer install

Na konci Vás instalátor provede nastavením databáze a dalších parametrů. Než dokončíte nastavení těchto parametrů, vytvořte ručně databázi (např. pomocí Admineru, PhpMyAdmin nebo z konzole). Jinak dojde na konci instalace k chybě: `SQLSTATE[HY000] [1049] Unknown database 'sonata-demo'` 

### Po dokončení `composer install` spusťte následující příkazy:

    php app/console doctrine:schema:update --force

#### 1. Instalace stylů, javascriptů apod.:

    php app/console assets:install

Pro Linux je lepší `php app/console assets:install --symlink`

Ze srandy můžete tento příkaz spustit jako `php app/console ass:in` :-))

#### 2. Vytvoření uživatele administrace (vyplníte uživatelské jméno, email a heslo [pozor heslo je viditelné]):

    php app/console fos:user:create --super-admin

#### 3. Spuštění zabudovaného Symfony serveru (pokud nechcete konfigurovat Apache):

    php app/console server:run

Následně si na adrese [http://localhost:8000/app_dev.php/admin](http://localhost:8000/app_dev.php/admin) zobrazíte administraci.

###### Příjemnou zábavu :-)
