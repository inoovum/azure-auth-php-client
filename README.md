# PHP client for azure authentication

PHP client for azure authentication

## Installation

Just run

```
composer require steinbauerit/azure-auth-php-client
```

## Usage

```injectablephp
try {
    $clientId = 'clientId';
    $clientSecret = 'secret';
    $authorizationCode = 'authCode';

    $tenantId = 'common';
    $redirectUri = 'http://localhost';

    // The auth provider will only authorize requests to
    // the allowed hosts, in this case Microsoft Graph
    $allowedHosts = ['graph.microsoft.com'];
    $scopes = ['User.Read'];

    $tokenRequestContext = new AuthorizationCodeContext(
        $tenantId,
        $clientId,
        $clientSecret,
        $authorizationCode,
        $redirectUri
    );

    $authProvider = new PhpLeagueAuthenticationProvider($tokenRequestContext, $scopes, $allowedHosts);
    $requestAdapter = new GuzzleRequestAdapter($authProvider);
    $client = new GraphApiClient($requestAdapter);

    $me = $client->me()->get()->wait();
    echo "Hello {$me->getDisplayName()}, your ID is {$me->getId()}";

} catch (ApiException $ex) {
    echo $ex->getMessage();
}
```


## Author

* E-Mail: patric.eckhart@steinbauer-it.com
* URL: http://www.steinbauer-it.com
