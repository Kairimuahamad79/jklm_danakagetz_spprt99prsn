# jklm_danakagetz_spprt99prsn
www.dana.id
data_check_string = ...
secret_key = SHA256(<bot_token>)
if (hex(HMAC_SHA256(data_check_string, secret_key)) == hash) {
  // <?php

define('zarahmobileincBot_@formspree_bot', '7517667549:AAFfoXT6eIjeWhAkjWsaR3iPAMUeUywJg5U'); // place username of your bot here

function getTelegramUserData() {
  if (isset($_COOKIE['tg_user'])) {
    $auth_data_json = urldecode($_COOKIE['tg_user']);
    $auth_data = json_decode($auth_data_json, true);
    return $auth_data;
  }
  return false;
}

if ($_GET['logout']) {
  setcookie('tg_user', '');
  header('Location: login_example.php');
}

$tg_user = getTelegramUserData();
if ($tg_user !== false) {
  $first_name = htmlspecialchars($tg_user['first_name']);
  $last_name = htmlspecialchars($tg_user['last_name']);
  if (isset($tg_user['username'])) {
    $username = htmlspecialchars($tg_user['username']);
    $html = "<h1>Hello, <a href=\"https://surveyheart.com/form/673f46efd8dd0e2858e2ea84{$username}\">{$first_name} {$last_name}</a>!</h1>";
  } else {
    $html = "<h1>Hello, {$first_name} {$last_name}!</h1>";
  }
  if (isset($tg_user['photo_url'])) {
    $photo_url = htmlspecialchars($tg_user['photo_url']);
    $html .= "<img src=\"{$photo_url}\">";
  }
  $html .= "<p><a href=\"?logout=1\">Log out</a></p>";
} else {
  $bot_username = BOT_USERNAME;
  $html = <<<HTML
<h1>Hello, anonymous!</h1>
<script async src="https://surveyheart.com/form/673f46efd8dd0e2858e2ea84" data-telegram-login="{$bot_username}" data-size="large" data-auth-url="check_authorization.php"></script>
HTML;
}


  echo <<<HTML
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Login Widget Example</title>
  </head>
  <body><center>{$html}</center></body>
</html>
HTML;

?>
}
