Connect With Google (Login in website by google mail account)
===================

Connect With Google
---------------------

Google APIs Client Library for PHP

1) Download source code files

2) Extract the library from the archive and copy the google-api-php-client directory to your project root.

3) Include and use the library in your project or take a look at an example under google-api-php-client/examples/plus. 

<?php
require_once 'google-api-php-client/src/Google_Client.php';
require_once 'google-api-php-client/src/contrib/Google_PlusService.php';

// Set your cached access token. Remember to replace $_SESSION with a
// real database or memcached.
session_start();

$client = new Google_Client();
$client->setApplicationName('Google+ PHP Starter Application');
// Visit https://code.google.com/apis/console?api=plus to generate your
// client id, client secret, and to register your redirect uri.
$client->setClientId('insert_your_oauth2_client_id');
$client->setClientSecret('insert_your_oauth2_client_secret');
$client->setRedirectUri('insert_your_oauth2_redirect_uri');
$client->setDeveloperKey('insert_your_simple_api_key');
$plus = new Google_PlusService($client);

if (isset($_GET['code'])) {
  $client->authenticate();
  $_SESSION['token'] = $client->getAccessToken();
  $redirect = 'http://' . $_SERVER['HTTP_HOST'] . $_SERVER['PHP_SELF'];
  header('Location: ' . filter_var($redirect, FILTER_SANITIZE_URL));
}

if (isset($_SESSION['token'])) {
  $client->setAccessToken($_SESSION['token']);
}

if ($client->getAccessToken()) {
  $activities = $plus->activities->listActivities('me', 'public');
  print 'Your Activities: <pre>' . print_r($activities, true) . '</pre>';

  // We're not done yet. Remember to update the cached access token.
  // Remember to replace $_SESSION with a real database or memcached.
  $_SESSION['token'] = $client->getAccessToken();
} else {
  $authUrl = $client->createAuthUrl();
  print "<a href='$authUrl'>Connect Me!</a>";
}


Sources Provided from: https://code.google.com/p/google-api-php-client/

Thanks to The Google Team

--------------------------------------------------------------
https://code.google.com/p/google-api-php-client/wiki/Samples
--------------------------------------------------------------
