# BuscaCEP.cmp

<aura:component implements="force:lightningQuickActionWithoutHeader,force:hasRecordId"
                controller="BuscaCEPController"> <!-- ADD PARA QUE A COMUNICAÇÃO COM LWC FUNCIONE https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/controllers_server_actions_call.htm-->
    <aura:attribute name="recordId" type="String" /> <!--ATRIBUTO -->
    <aura:attribute name="CEP" type="String" /> <!-- ATRIBUTO -->
     <aura:attribute name="retornoViaCEP" type="Object" /> <!-- ATRIBUTO PARA INSERIR OS VALORES NA TELA -->
    <!-- ... -->
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    
    <aura:html tag="style">
        .botaoIcone.slds-p-around_small.slds-size_6-of-12{
        	margin-top: 27px !important;
        }
    </aura:html> <!-- ALINHAMENTO DO ICONE SEARCH -->

    
    <header class="slds-modal__header"> <!-- FORMATO DA JANELA ABERTA DOC DEVSALESFORCE https://www.lightningdesignsystem.com/components/modals/ -->      
        <h2 id="modal-heading-01" class="slds-modal__title slds-hyphenate">Busca Endereço</h2>       
    </header>
    <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
         <lightning:layout multipleRows="true" >  <!-- COLOCA TRUE PARA QUEBRAR LINHA NA 12º COLUNA -->
             <!-- Linha 1 -->
             <lightning:layoutItem padding="around-small" size="6"> <!-- LAYOUTITEM PARA DAR O COMANDO DE SIZE = 6 PARA TER 2 COLUNAS EM CADA LINHA-->
                 <lightning:input name="cep" label="CEP" value="{!v.CEP}" /> <!-- COLOCAR VALOR NO INPUT -->
             </lightning:layoutItem>
             <lightning:layoutItem padding="around-small" size="6" class="botaoIcone">
                 <!-- BUTTON ICON ACEITA QUE COLOCA UM ICONE NELE https://developer.salesforce.com/docs/component-library/bundle/lightning:buttonIcon/example-->
                     <lightning:buttonIcon iconName="utility:search" variant="bare" alternativeText="busca"
                                           onclick="{!c.buscarCEP}"/> <!-- UTILITY PARA COLOCAR O ICONE  https://www.lightningdesignsystem.com/icons/ -->
             </lightning:layoutItem>   <!-- ONCLICK PARA QUANDO CLICAR NA LUPA ABRIR VALOR -->
             							
             <!-- Linha 2 -->
             <lightning:layoutItem padding="around-small" size="6">
                  <lightning:input name="rua" label="Rua" value="{!v.retornoViaCEP.logradouro}"  />
             </lightning:layoutItem>									<!-- ATRIBUTO -->
             <lightning:layoutItem padding="around-small" size="6">
                  <lightning:input name="Bairro" label="Bairro"  value="{!v.retornoViaCEP.bairro}" /> 
             </lightning:layoutItem> <!-- HABILITA VALORES PARA SEREM INSERIDOS APOS DIGITAR CEP BASEADO NO JSON -->
             
             <!-- Linha 3 -->
             <lightning:layoutItem padding="around-small" size="6">
                 <lightning:input name="Cidade" label="Cidade"  value="{!v.retornoViaCEP.localidade}" />
             </lightning:layoutItem>
             <lightning:layoutItem padding="around-small" size="6">
                 <lightning:input name="Estado" label="Estado"  value="{!v.retornoViaCEP.uf}" />
             </lightning:layoutItem>
        </lightning:layout>
    </div>
    <footer class="slds-modal__footer">
        												<!-- ONCLICK FUNÇÃO -->
        <button class="slds-button slds-button_neutral" onclick="{!c.cancelar}" >Cancelar</button> <!-- QUANDO APERTA CANCELAR FECHA JANELA https://developer.salesforce.com/docs/component-library/bundle/force:closeQuickAction/documentation -->
        <button class="slds-button slds-button_brand" onclick="{!c.salvarEndereco}">Salvar</button>
    </footer>
    
</aura:component>
