# Azure-VM-Naming-Convention---Padrao-de-Nomes
Padronize a nomenclatura de suas VM's com o Azure Custom Policy

Essa Azure Custom Policy impõe um padrão de nomenclatura para Máquinas Virtuais (VMs) no Azure. Vamos analisar os parâmetros principais:

Propriedades Gerais:
{
  "displayName": "VM - padrao de nomenclatura",
  "policyType": "Custom",
  "mode": "All",
  "version": "1.0.0"
}

displayName: Nome amigável da política, indicando que ela define um padrão de nomenclatura para VMs.
policyType: Custom significa que essa política foi criada pelo usuário, não é uma das políticas padrão da Microsoft.
mode: All significa que a política pode ser aplicada tanto a recursos existentes quanto a novos.
version: Indica a versão da política.

Regras da Política (policyRule)
A política usa uma condição if para verificar se a VM segue o padrão de nomenclatura. Se não seguir, o then bloqueia a criação.

Condição (if)

"if": {
  "allOf": [
    {
      "field": "type",
      "equals": "Microsoft.Compute/virtualMachines"
    },
    {
      "allOf": [
        {
          "field": "name",
          "notMatch": "vm-????-...-###"
        }
      ]
    }
  ]
}

field: "type", equals: "Microsoft.Compute/virtualMachines"

Aplica-se apenas a VMs.
field: "name", notMatch: "vm-????-...-###"

O nome da VM deve seguir um padrão específico.
"notMatch" significa que, se o nome da VM não seguir esse padrão, a regra será acionada.
O padrão "vm-????-...-###" provavelmente representa:
vm- → Prefixo fixo.
???? → Quatro caracteres obrigatórios (letras ou números).
... → Pode indicar um conjunto de caracteres obrigatórios.
### → Três números obrigatórios.

Ação (then)
"then": {
  "effect": "deny"
}

effect: "deny" impede a criação da VM se ela não seguir o padrão de nomenclatura.

A política força um padrão de nomenclatura para Máquinas Virtuais (VMs) no Azure.
Se o nome da VM não seguir o formato "vm-????-...-###", a criação será negada.
Isso ajuda a manter um padrão organizacional e facilitar a identificação das VMs.

########################################################################################################


# Azure-VM-Naming-Convention---Naming-Pattern
Standardize your VMs' naming with Azure Custom Policy

This Azure Custom Policy enforces a naming standard for Virtual Machines (VMs) in Azure. Let's analyze the main parameters:

General Properties:
{
  "displayName": "VM - padrao de nomenclatura",
  "policyType": "Custom",
  "mode": "All",
  "version": "1.0.0"
}

displayName: Friendly name of the policy, indicating that it defines a naming standard for VMs.
policyType: Custom means that this policy was created by the user, it is not one of the default Microsoft policies.
mode: All means that the policy can be applied to both existing and new resources.
version: Indicates the version of the policy.

Policy Rules (policyRule)
The policy uses an if condition to check if the VM follows the naming pattern. If it does not, the then blocks the creation.

Condition (if)

"if": {
  "allOf": [
    {
      "field": "type",
      "equals": "Microsoft.Compute/virtualMachines"
    },
    {
      "allOf": [
        {
          "field": "name",
          "notMatch": "vm-????-...-###"
        }
      ]
    }
  ]
}

field: "type", equals: "Microsoft.Compute/virtualMachines"

Applies to VMs only.
field: "name", notMatch: "vm-????-...-###"

The VM name must follow a specific pattern. "notMatch" means that if the VM name does not follow this pattern, the rule will be triggered.
The pattern "vm-????-...-###" probably represents:
vm- → Fixed prefix.
???? → Four mandatory characters (letters or numbers).
... → Can indicate a set of mandatory characters.
### → Three mandatory numbers.

Action (then)
"then": {
  "effect": "deny"
}

effect: "deny" prevents the creation of the VM if it does not follow the naming pattern.

The policy enforces a naming pattern for Virtual Machines (VMs) in Azure.
If the VM name does not follow the format "vm-????-...-###", creation will be denied.
This helps maintain an organizational standard and makes it easier to identify VMs.
