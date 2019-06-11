#说明#
    这是我在unionpay实习期间写的一个邮件系统。主要包括了一个邮件发送的客户端以及邮件发送的服务端。感谢pOny老师 对我在unionpay实习期间的照顾，我才能够顺利的写完这个系统。在unionpay实习期间，我学到了很多开发方面的知识，虽然我没有能够留在unionpay，但是，我非常感恩在unionpay度过的这段日子。仅以此系统纪念我的在unionpay实习的这段难忘的经历。
    本系统主要基于phpmailer进行二次开发。在原有的基础上，实现了邮件服务器后端及前端方面的优化。

#这个系统开发的初衷#
    许多PHP开发人员在代码中使用电子邮件。唯一支持此功能的PHP函数是“mail（）”函数。但是，它不提供任何帮助来使用流行的功能，如基于HTML的电子邮件和附件。正确格式化电子邮件是非常困难的。有无数的重叠的RFC，需要严格遵守极其复杂的格式和编码规则——您将在网上找到的绝大多数直接使用“mail（）”函数的代码都是完全错误的！希望这个系统能够给初学者一些启示。

#目前支持的开源cms有#：
```
wordpress，
drupal，
1crm，
sugarcrm，
yii，
joomla
...
```

#以下是其中的一个简单例子#
```
<?php
// Import PHPMailer classes into the global namespace
// These must be at the top of your script, not inside a function
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;

// Load Composer's autoloader
require 'vendor/autoload.php';

// Instantiation and passing `true` enables exceptions
$mail = new PHPMailer(true);

try {
    //Server settings
    $mail->SMTPDebug = 2;                                       // Enable verbose debug output
    $mail->isSMTP();                                            // Set mailer to use SMTP
    $mail->Host       = 'webmail.unionpay.com;';  // Specify main and backup SMTP servers
    $mail->SMTPAuth   = true;                                   // Enable SMTP authentication
    $mail->Username   = 'webmail@unionpay.com';                     // SMTP username
    $mail->Password   = 'unionpaysecret';                               // SMTP password
    $mail->SMTPSecure = 'tls';                                  // Enable TLS encryption, `ssl` also accepted
    $mail->Port       = 587;                                    // TCP port to connect to

    //Recipients
    $mail->setFrom('from@unionpay.com', 'Mailer');
    $mail->addAddress('joe@unionpay.com', 'Joe User');     // Add a recipient
    $mail->addAddress('ellen@unionpay.com');               // Name is optional
    $mail->addReplyTo('info@unionpay.com', 'Information');
    $mail->addCC('cc@unionpay.com');
    $mail->addBCC('bcc@unionpay.com');

    // Attachments
    $mail->addAttachment('/var/tmp/file.tar.gz');         // Add attachments
    $mail->addAttachment('/tmp/image.jpg', 'new.jpg');    // Optional name

    // Content
    $mail->isHTML(true);                                  // Set email format to HTML
    $mail->Subject = 'Here is the subject';
    $mail->Body    = 'This is the HTML message body <b>in bold!</b>';
    $mail->AltBody = 'This is the body in plain text for non-HTML mail clients';

    $mail->send();
    echo 'Message has been sent';
} catch (Exception $e) {
    echo "Message could not be sent. Mailer Error: {$mail->ErrorInfo}";
}
/*
测试地址：http://webmail.unionpay.com
测试账号：
username:test
password:unionpay123!
*/
```

#更新记录#
```
1、集成的SMTP支持-不使用本地邮件服务器发送
2、发送包含多个收件人、抄送、密件抄送和回复地址的电子邮件
3、不阅读HTML电子邮件的邮件客户端的多部分/备选电子邮件
4、添加附件，包括内联
5、支持UTF-8内容和8bit、base64、二进制和带引号的可打印编码
6、通过ssl和smtp+starttls传输使用login、plain、cram-md5和xoath2机制进行的SMTP身份验证
7、自动验证电子邮件地址
8、防止收割台注入攻击
9、超过50种语言的错误消息！
10、支持DKIM和S/MIME签名
11、与php 5.5及更高版本兼容
12、引入命名空间以防止名称冲突
```
