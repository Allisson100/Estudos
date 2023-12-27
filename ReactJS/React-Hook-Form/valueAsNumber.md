# Finalizando cadastro

Mudamos alguns nomes do inputs, pois estavamos dando um nome no input como nome, mas nosso objeto tinha que ser titulo, então mudamos isso. E também adiconamos uma configuração a mais no input:

    <input {...register('preco', { required: true, valueAsNumber: true })} type="number" placeholder="Preço do produto" />

Nesse caso estavamos pegando o número como uma string, mas o nosso objeto precisa receber isso como um número para podermos utilizar o .toFixed. Então colocamos o alueAsNumber: true, que vem do react-hook-form, que já transforma esse dado de string para number para nós.

