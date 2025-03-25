# Repte

## Descripció

* Es tracta d'aconseguir endevinar un número amagat a partir de pistes.
* Les pistes les ofereix una API.

## Adreça de la API

* La API és a l'ordinador del professor, la publicarà aquí:


https://f5e3-85-192-74-3.ngrok-free.app

## Informació addicional

* A la pàgina se li ha eliminat el `app.UseSwaggerUI();`. Però, amb OpenApi, encara pots saber quins endpoints hi ha.
* Aquesta documentació t'ajudarà a descobrir com trobar endpoints: [Add and configure Swagger middleware](https://learn.microsoft.com/en-us/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-8.0&tabs=visual-studio#add-and-configure-swagger-middleware)


## Com ho fa el professor per compartir?

```bash
ngrok http 5040
```

## Posershell per fer la crida a la APO

```powershell
$headers = @{
    "accept" = "application/json"
    "Content-Type" = "application/json"
}

$body = @{
    valor = 0
} | ConvertTo-Json

Invoke-RestMethod -Uri "https://f5e3-85-192-74-3.ngrok-free.app/????" -Method Post -Headers $headers -Body $body
```