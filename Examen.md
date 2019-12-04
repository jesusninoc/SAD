```PowerShell
$passactu = "system"

$pass=Read-Host 'Introducir contraseña para acceder al sistema'
if($pass -eq $passactu){
 'Acceso Permitido'
 function menu_vuelos
{
param (
[string]$Title = 'Menú'
)
cls
Write-Host "================ $Title ================"
 
Write-Host "1: Ver actualizaciones"
Write-Host "2: Ver informacion sobre el hardware y software"
Write-Host "3: Ver la información descifrada"
Write-Host "4: Comprobar el hash del fichero"
Write-Host "5: Asistente de contraseñas y cifarlas"
Write-Host "6: Presiona 'S' para salir."
}

do
{
menu_vuelos
$input = Read-Host "Selecciona una opción"
switch ($input)
{
'1' {
cls

Write-Host
'-->A continuación se le mostrará un lista con las actualizaciones'
Write-Host
Get-HotFix | Select-Object HotFixID
Get-Package | Select-Object Name | Where-Object Name -match "Actualización" | Format-Custom
}

 '2' {
cls
Write-Host
'-->A continuación se le mostrará un lista con la información del Hardware y el Software'
Write-Host
 Get-Content inf.txt
} 


'3' {
cls
'-->Ha seleccionado la opción de ver el fichero descifrado'
$fichero = gc inf.txt
$cadena='$fichero'
$clave='clavesecreta123'

$clavebyte=[Byte[]]($clave.PadRight(24).Substring(0,24).ToCharArray())

$cadenacifrada=$cadena | ConvertTo-SecureString -AsPlainText -Force | ConvertFrom-SecureString -Key $clavebyte
$cadenacifrada
$fichero

'Este es el fichero descifrado'
}

'4' {
cls
#A veces no muestra el hash y hay que volver a seleccionar la opción
'-->Ha seleccionado la opción de comprobar el hash del fichero'
$hash = Get-FileHash C:\Users\Administrador\inf.txt -Algorithm SHA512 
$hash
    if ($hash -eq $hash){
        'El fichero no se ha modificado.'
        
   
    }
    else{
        'Alerta ! el fichero se ha modificado'
    }

}


'5' {
cls
'-->Si es correcta se le cifrará'
$pass=Read-Host -AsSecureString 'Introducir contraseña para comprobar la longitud'
if($pass.Length -lt 10){
'La contraseña es corta'
}
else{
'La contraseña es correcta según la longitud'
[Reflection.Assembly]::LoadWithPartialName("System.Web")

$password=Read-Host 'Introduce de nuevo la contraseña para cifrarla'

"Hash MD5"
$contra = [System.Web.Security.FormsAuthentication]::HashPasswordForStoringInConfigFile($pass, "MD5")
$contra

}

}

's' {
return
}
}
pause
}
until ($input -eq 's')
}
else{
'Acceso Denegado'

'¿Quieres comprobar que tu IP da respuesta?'


$ip = Read-Host "Escriba su dirección IP"  
$ping = ping $ip

$haceping = $ping

if($haceping -ne $ping){
    "La direccion IP da respuesta"
    $ping 
} else {
    "La direcicon IP no es válida"
}



}
```
