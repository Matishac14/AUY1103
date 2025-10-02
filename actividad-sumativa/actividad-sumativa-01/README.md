# README.md

Este repositorio define una infraestructura modular en AWS usando Terraform. La estructura de carpetas y archivos es la siguiente:
````
├── README.md
├── main.tf
├── modules
│ ├── alb
│ │ ├── main.tf
│ │ ├── outputs.tf
│ │ └── variables.tf
│ ├── ec2
│ │ ├── main.tf
│ │ ├── outputs.tf
│ │ ├── user_data.sh.tpl
│ │ └── variables.tf
│ ├── security_group
│ │ ├── main.tf
│ │ ├── outputs.tf
│ │ └── variables.tf
│ └── vpc
│ ├── main.tf
│ ├── outputs.tf
│ └── variables.tf
├── outputs.tf
├── providers.tf
├── terraform.tfstate
├── terraform.tfvars
└── variables.tf
````
## Requisitos

- AWS CLI instalado y configurado.
- Terraform instalado 
- Git instalado y configurado.

## Configuración de AWS CLI

Antes de usar Terraform, configurar las credenciales de AWS disponibles en el laboratorio de AWS:
```bash
aws configure
```
```
Ingrese su AWS Access Key ID
Ingrese su AWS Secret Access Key
Región (por ejemplo, us-east-1)
Formato de salida (json)
```
o 

```bash
vim ~/.aws/credentials
```

## Variables

Edite `terraform.tfvars` para ajustar valores como nombres, CIDRs, tipo de instancia y tags, entre otros.

Ejemplo de `terraform.tfvars`:
````
aws_region          = "us-east-1"
project_name        = "cheese-factory"
environment         = "dev"
vpc_cidr            = "10.0.0.0/16"
public_subnet_cidrs = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
my_ip               = "0.0.0.0/0"
instance_type       = "t2.micro"
docker_images       = ["errm/cheese:wensleydale", "errm/cheese:cheddar", "errm/cheese:stilton"]
````




## Flujo de trabajo con Terraform

Desde la raíz del proyecto, ejecute los siguientes comandos:

1. **Inicializar** el directorio de trabajo de Terraform y descargar proveedores y módulos:
   ```bash
   terraform init
   ```


2. **Dar formato** a los archivos de Terraform:
   ```bash
   terraform fmt
   ```

3. **Validar** la configuración y detectar errores de sintaxis o referencias:
   ```bash
   terraform validate
   ```

4. **Revisar** el plan de ejecución sin aplicar cambios:
   ```bash
   terraform plan
   ```
5. **Aplicar** los cambios para crear la infraestructura:
   ```bash
   terraform apply
   ```

Confirmar con "yes" cuando se solicite

6. **Destruir** todos los recursos creados:
   ```bash
   terraform destroy
   ```

Confirmar con "yes" cuando se solicite

En caso de querer forzar tanto el apply como el destroy sin confirmación, se puede usar la opción `-auto-approve`:
```bash
terraform apply -auto-approve
```
```bash
terraform destroy -auto-approve
```

## Validaciones

Para validar el uso de ALB de forma correcta, es necesario dentro del navegador desactivar el cache, esto puede hacerse con clic derecho en inspeccionar > Network > Disable cache (mientras la consola de desarrollador esté abierta).
