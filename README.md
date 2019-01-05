Projet SMS:
1. Envoyer un SMS?
2.Recevoir un SMS?
3.Liste des Messages?

Fait attention  avec version …Mon Version est 6 Marshmallow
Le prémiere chose, il faut faire le xml

1.xml

EditText-editer des messages
ListView_lister des messages
Button(onclickable button)-Send(sont appelé le method onSendClick()

2.Manifest

<uses-permission android:name="android.permission.WRITE_SMS" />
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.SEND_SMS" />
<uses-permission android:name="android.permission.RECEIVE_SMS" />
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>

Après l'intérieur de receiver,j'ai ajouté l'intent filter pour recevoir les messages
<intent-filter android:priority="999" >
    <action android:name="android.provider.Telephony.SMS_RECEIVED" />
    <action android:name="android.intent.action.BOOT_COMPLETED"/>
</intent-filter>

Pour éviter d'avoir des multiple instances…j'ai ajouté dans le manifest….<android:launchmode="singleInstance">
3.Les Méthodes:

J'ai ajouté 2 methods pour demander le permission 

i)getPermissionToReadSMS():Vérifier cette site pour plus de explications
(https://developer.android.com/reference/android/support/v4/app/ActivityCompat.html)
Dans cette méthode,il vérifie que le permission est bien accordé ou pas pour lire un SMS
ii)onRequestPermissionResult()…..Vérifier le site pour l'explication

Méthodes pour button et liste des messages

iii)onSendClick()(Button Send)
   il faut  demander le permission pour lire un SMS et aussi j'ai ajouté le numéro(si vous voulez,vous pouvez ajouter votre numéro) pour envoyer un message.
iv)refreshsmsInbox()…(refrachir de sms pour lister les nouveaux messages).J'ai ajouté
    -ContentResolver-globale instanciation dans l'application qui donne l'acess
    -Cursor-j'ai fait le url(pour avoir des messages dans l'Inbox)
 v)Update Inbox()  ….pour faire le mis à jour dans l'Inbox
  vi)onStart()….pour commencer
  vii)on Stop()….pour arrêter



4.Classe SMSReceiver:(c'est fait comme new->Other_>Broadcast Receiver)
 
•	Les SMS sont contenus dans l'attribut extras qui est de type Bundle.
•	Un Bundle est une sorte de map dont les clés sont un nom(String)et les valeurs des objets Parcelable(équivalent de Serializable dans le monde Android),La valeur intéressante ici est indexée par le nom<<pdus>>
•	PDU signifie Protocol Description Unit,c'est un format utilisé pour encoder les SMS.On passe alors du tableau d'octets représentât les données brute à l'objet SmsMessage par le méthode statique createFromPdu.
•	La manipulation du SMS est ensuite aisée grâce aux méthodes dont dispose cette  classe.



  
 



