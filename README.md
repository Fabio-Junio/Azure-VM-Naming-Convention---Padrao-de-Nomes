# Azure-VM-Naming-Convention-Padrao-de-Nomes

**Padronize a nomenclatura de suas VM's com o Azure Custom Policy**

O Azure Custom Policy faz parte do Azure Policy, um serviço que ajuda a gerenciar e aplicar governança nos recursos do Azure. 
O Azure Policy permite criar, atribuir e gerenciar políticas para garantir que os recursos estejam em conformidade com os requisitos organizacionais. 
O Custom Policy refere-se às políticas personalizadas que você pode criar quando as políticas internas do Azure não atendem às suas necessidades específicas.

Essa Azure Custom Policy impõe um padrão de nomenclatura para Máquinas Virtuais (VMs) no Azure. Vamos analisar os parâmetros principais:

### Propriedades Gerais:
```json

{
  "displayName": "VM - padrao de nomenclatura",
  "policyType": "Custom",
  "mode": "All",
  "version": "1.0.0"
}
```
displayName: Nome amigável da política, indicando que ela define um padrão de nomenclatura para VMs.

policyType: Custom significa que essa política foi criada pelo usuário, não é uma das políticas padrão da Microsoft.

mode: All significa que a política pode ser aplicada tanto a recursos existentes quanto a novos.

version: Indica a versão da política.

Regras da Política (policyRule)
A política usa uma condição if para verificar se a VM segue o padrão de nomenclatura. Se não seguir, o then bloqueia a criação.

Condição (if)
```json
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
```
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
```json
"then": {
  "effect": "deny"
}
```
effect: "deny" impede a criação da VM se ela não seguir o padrão de nomenclatura.

Resumo
A política força um padrão de nomenclatura para Máquinas Virtuais (VMs) no Azure.

Se o nome da VM não seguir o formato "vm-????-...-###", a criação será negada.

Isso ajuda a manter um padrão organizacional e facilitar a identificação das VMs.

```
