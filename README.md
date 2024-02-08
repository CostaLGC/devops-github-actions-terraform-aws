# DevOps GitHub Actions Terraform AWS

Automatize e gerencie sua infraestrutura na AWS com GitHub Actions e Terraform! Este repositório oferece workflows prontos para uso que integram poderosas ferramentas de automação, permitindo que você provisione e gerencie recursos na nuvem de forma eficiente.

## Recursos

- Projetado para acelerar o desenvolvimento e a entrega contínua (CI/CD).
- Configuração fácil e pronta para uso com Terraform e AWS.
- Fluxos de trabalho personalizáveis para atender às suas necessidades específicas de DevOps.
- Ensina boas práticas para aplicação e remoção de recursos com Terraform, incluindo etapas detalhadas para o `apply` e o `destroy`.
- Utiliza um provider Terraform para se conectar à AWS e gerenciar recursos na nuvem.


## Configuração do Provider

A primeira etapa ao trabalhar com Terraform é a configuração do provider, responsável por comunicar-se com o provedor de nuvem (no nosso caso, a AWS) e realizar operações nos recursos. Para isso, utilizamos o bloco `provider` no código Terraform. 

No Terraform, o provedor (`provider`) é uma parte fundamental que estabelece a conexão com um provedor de nuvem, como a AWS, Azure, Google Cloud, entre outros. Para que o Terraform possa interagir com a infraestrutura na nuvem, é necessário configurar corretamente o provedor, o que inclui fornecer credenciais de acesso.

As credenciais de acesso são necessárias para autenticar-se na nuvem e realizar operações nos recursos. No caso específico da AWS, as credenciais de acesso são geralmente compostas por um ID de chave de acesso (`Access Key ID`) e uma chave de acesso secreta (`Secret Access Key`).

Essas credenciais podem ser configuradas de várias maneiras, incluindo o uso de arquivos de configuração locais, variáveis de ambiente, ou, em ambientes de nuvem, associando uma IAM Role à instância onde o Terraform está sendo executado.

Veja um exemplo:

```hcl
provider "aws" {
  region = "us-east-1"
}
```
No exemplo abaixo, podemos ver como as credenciais de acesso à AWS são configuradas como variáveis de ambiente em um workflow do GitHub Actions:

```yaml
jobs:
  meu_job:
    runs-on: ubuntu-latest
    env:
      TF_VERSION: "1.0.11"
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

```

## Como Usar

1. Faça um fork deste repositório.
2. Clone o fork para o seu ambiente local.
3. Configure as variáveis de ambiente necessárias no GitHub.
4. Personalize os workflows conforme necessário para o seu projeto.

## Contribuindo

Sinta-se à vontade para contribuir com melhorias, correções de bugs ou novos recursos! Basta abrir uma issue ou enviar uma pull request.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
