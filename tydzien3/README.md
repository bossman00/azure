# azure
kurs azure 


#TYDZIEN3.1 „Zbuduj prostą konwencję nazewniczą dla min. takich zasobów jak Grupa Zasobów, VNET, Maszyn Wirtualna, Dysk, Konta składowania danych. Pamiętaj o ograniczeniach w nazywaniu zasobów, które występują w Azure”
https://github.com/bossman00/azure/tree/master/tydzien3/1

      




#TYDZIEN3.2 „ Zbuduj prosty ARM Template (możesz wykorzystać już gotowe wzorce z GitHub), który wykorzystuje koncepcję Linked Templates. Template powinien zbudować środowisko złożone z jednej sieci VNET, podzielonej na dwa subnety. W każdy subnecie powinna powstać najprostsza maszyna wirtualna z systemem Ubuntu 18.04 a na każdym subnecie powinny zostać skonfigurowane NSG.”
#TYDZIEN3.4 „Spróbuj na koniec zmodyfikować template tak, by nazwa użytkownika i hasło do każdej maszyny z pkt. 2 było pobierane z KeyVault.„
az group create --name tydzien3rg --location westeurope
az keyvault create --name 'bossKVtydzien3' --resource-group 'tydzien3rg' --location westeurope
az provider register -n Microsoft.KeyVault
az keyvault secret set --vault-name 'bossKVtydzien3' --name 'bosstydzien3vmAdminUserPass' --value 'Pa$$w0rd'
az keyvault secret set --vault-name 'bossKVtydzien3' --name 'bosstydzien3vmAdminUserName' --value 'bossadmin'
az keyvault update --name 'bossKVtydzien3' --resource-group 'tydzien3rg' --enabled-for-deployment 'true'
az keyvault update --name 'bossKVtydzien3' --resource-group 'tydzien3rg' --enabled-for-disk-encryption 'true'
az keyvault update --name 'bossKVtydzien3' --resource-group 'tydzien3rg' --enabled-for-template-deployment 'true'
az group deployment create --resource-group tydzien3rg --template-uri https://raw.githubusercontent.com/bossman00/azure/master/tydzien3/2/azuredeploy.json --parameters @kv.parameters.json  --name bosstydzien32



#TYDZIEN3.3 „Zbuduj najprostrzą właśną rolę RBAC, która pozwala użytkownikowi uruchomić maszynę, zatrzymać ją i zgłosić zgłoszenie do supportu przez Portal Azure”



