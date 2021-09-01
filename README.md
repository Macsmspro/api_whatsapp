`1- URL API`

L' API est appelée par l'url "https://macsmspro.com/api/whatsapp.php" . Il autorise les requetes `POST` et requiert en body un token directement lié à votre compte grâce auquel les envois sont effectués.


`2- CORPS DE LA REQUETE`

`Le Nom`
Il s'agit du nom que portera le message. Il a les propriétés de ne pas être NULL ou vide, et doit pas excéder plus de dix (10) caratères. Désigné dans le corps de la reqête par name.

`Le Message`
Il n'est rien d'autre que le contenu du message à envoyer. Reconnu dans le corps de la requête par la propriété message, il est requis et ne peut donc être NULL ou vide.

`Le téléphone`
Il représente le numéro de téléphone destinataire, il doit être suvi de son indicatif, ne doit contenir aucun espace et ne peut être NULL ou vide.
Ex: 229xxxxxxxx Désigné dans le corps de la reqête par telephone

`Les fichers attachés`
Il s'agit de la liste des fichers attachés au message MMS, de type array il contient les urls vers chaque fichers. Ce champ à la capacité d'être optionnel

`Le token`
Il est question du token que vous avez généré pour votre compte, il est requis pour tout envoi vers API. Il est utilisé dans le corps de reqête sous le même nom.

Lorsque les critères d'une donnée ne sont pas vérifiés une erreur de type 422 est retournéé. Vous retrouverez les détails sur les types d'erreurs dans la section suivante.

`3- REPONSES DU SERVEUR`

Le serveur retourne deux catégories possible de réponse lors d'une rêquete. Nous avons les retours de type ERROR et les retours de type SUCCESS.
Les messages d'erreur
Les messages d'erreur sont sous le format:
`"error" : {
"message" : {
"nom de l'erreur" : "message d'erreur"
}
}`
OU
`"error" : {
"message" : "message d'erreur"
}`
OU
`"error" : {
"messages" : [
{
"nom_erreur" : "message d'erreur"
}
]
}`

`Quelques erreurs`

`"error" : {
"message" : "Method Not Allowed"
}`
Cette erreur est retournée avec un code `405` lorsque la requete envoyée n'est pas de type `POST`
`"error" : {
"message" : "Crédit insuffisant"
}`
Cette erreur est retournée avec un code `403` lorsque le compte utilisateur ne dispose pas d'assez de crédit pour effectuer l'opération.
`"error" : {
"message" : "Message whatsapp non envoyé à xxx . Veuillez valider votre nom d'activité yyy"
}`
Cette erreur est retournée avec un code `400` lorsque les procédures de configuration du whatsapp sender n'ont pas été achevé
`"error" : {
"message" : {
"token" : "Le token est requis"
}
}`
Cette erreur est retournée avec un code `422` lorsque la valeur du token est vide ou NULL
`"error" : {
"message" : {
"token" : "token invalid"
}
}`
Cette erreur est retournée avec un code `401` lorsque la valeur du token envoyée ne correspond à aucun compte utilisateur du système.
`"error" : {
"messages" : [
{
"telephone" : "Le numéro de téléphone destinataire est requis"
}
]
}`
Cette erreur est retournée avec un code `422` lorsque la valeur du numero de telephone est vide ou `NULL`
`"error" : {
"messages" : [
{
"message" : "Le corps du message est requis"
}
]
}`
Cette erreur est retournée avec un code `422` lorsque la valeur du message est vide ou `NULL`
`"error" : {
"messages" : [
{
"name" : "Le nom est requis"
}
]
}`
Cette erreur est retournée avec un code `422` lorsque la valeur du nom est vide ou `NULL`
Plusieurs messages d'erreur peuvent se briquer comme suit
`"error" : {
"messages" : [
{
"name" : "Le nom est requis"
}, {
"telephone" : "Le numéro de téléphone destinataire est requis"
}, {
"message" : "Le corps du message est requis"
}
}`
Cette erreur est retournée avec un code `422` lorsque plusieurs données ne sont pas vérifiées à la fois `NULL`
Les messages de réussite
`"success" : {
"message" : "Message whatsapp envoyé avec succès au 229xxxxxxxx"
}`

Cette réponse est retournée avec un code` 200` lorsque le message a été envoyé sans aucun problème rencontré.



`La taille totale des fichiers doit être inférieure ou égale à 5 MB`

`Créez un compte pour obtenir un token Macsmspro`
