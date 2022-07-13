# Importer les bibliothèques requises
importer des  pandas  en tant que  pd
 tiret d'importation
importer  dash_html_components  au  format html
importer  dash_core_components  en tant que  dcc
du  tiret . dépendances  importer  Input , Output
importer  complot . exprimer  en  px

# Lire les données de la compagnie aérienne dans la base de données pandas
espacex_df  =  pd . read_csv ( "spacex_launch_dash.csv" )
max_payload  =  spacex_df [ 'Masse de la charge utile (kg)' ]. maximum ()
min_payload  =  spacex_df [ 'Masse de la charge utile (kg)' ]. min ()

# Créer une application de tableau de bord
app  =  tiret . Tiret ( __nom__ )

# Créer une mise en page d'application
application . mise en page  =  html . Div ( children = [ html . H1 ( 'SpaceX Launch Records Dashboard' ,
                                        style = { 'textAlign' : 'center' , 'color' : '#503D36' ,
                                               'taille-police' : 40 }),
                                # TÂCHE 1 : Ajouter une liste déroulante pour activer la sélection du site de lancement
                                # La valeur de sélection par défaut est pour TOUS les sites
                                cc . Liste déroulante ( id = 'site-dropdown' ,
                                            choix = [
                                                { 'label' : 'Tous les sites' , 'value' : 'TOUS' },
                                                { 'étiquette' : 'CCAFS LC-40' , 'valeur' ​​: 'CCAFS LC-40' },
                                                { 'étiquette' : 'VAFB SLC-4E' , 'valeur' ​​: 'VAFB SLC-4E' },
                                                { 'étiquette' : 'KSC LC-39A' , 'valeur' ​​: 'KSC LC-39A' },
                                                { 'étiquette' : 'CCAFS SLC-40' , 'valeur' ​​: 'CCAFS SLC-40' },
                                            ],
                                            valeur = 'TOUS' ,
                                            placeholder = "Sélectionnez un site de lancement ici" ,
                                            consultable = Vrai
                                            ),
                                html . Br (),

                                # TÂCHE 2 : Ajoutez un graphique à secteurs pour afficher le nombre total de lancements réussis pour tous les sites
                                # Si un site de lancement spécifique a été sélectionné, affiche le nombre de réussites par rapport aux échecs pour le site
                                html . Div ( dcc . Graph ( id = 'success-pie-chart' )),
                                html . Br (),

                                html . P ( "Plage de charge utile (Kg):" ),
                                # TÂCHE 3 : Ajouter un curseur pour sélectionner la plage de charge utile
                                #dcc.RangeSlider(id='payload-slider',...)
                                cc . RangeSlider ( id = 'payload-slider' ,
                                                min = 0 , max = 10000 , pas = 1000 ,
                                                marques = { 0 : '0' , 2500 : '2500' , 5000 : '5000' , 7500 : '7500' , 10000 : '10000' },
                                                valeur = [ min_payload , max_payload ]),
                                # TÂCHE 4 : Ajouter un nuage de points pour montrer la corrélation entre la charge utile et le succès du lancement
                                html . Div ( dcc . Graph ( id = 'success-payload-scatter-chart' )),
                                ])

# TÂCHE 2 :
# Ajouter une fonction de rappel pour `site-dropdown` en entrée, `success-pie-chart` en sortie
# Décorateur de fonction pour spécifier l'entrée et la sortie de la fonction
@application . _ callback ( Sortie ( component_id = 'success-pie-chart' , component_property = 'figure' ),
              Entrée ( component_id = 'site-dropdown' , component_property = 'value' ))
def  get_pie_chart ( enter_site ):
     filtered_df =  spacex_df
    si  enter_site  ==  'ALL' :
        figue  =  px . tarte ( filtered_df , valeurs = 'classe' ,
        names = 'Site de lancement' ,
        title = 'Total Success Launches By Site' )
        retour  figue
    sinon :
        # renvoie le graphique des résultats pour un site sélectionné
         filtered_df =  spacex_df [ spacex_df [ 'Lancer le site' ] == enter_site ] 
        filtered_df  =  filtered_df . groupby ([ 'Lancer le site' , 'classe' ]). taille (). reset_index ( nom = 'nombre de classes' )
        figue  =  px . tarte ( filtered_df , values ​​= 'class count' ,
        noms = 'classe' ,
        title = f'Succès total lancé pour le site { enter_site } ' )
        retour  figue
# TÂCHE 4 :
# Ajouter une fonction de rappel pour `site-dropdown` et `payload-slider` comme entrées, `success-payload-scatter-chart` comme sortie
@application . _ callback ( Sortie ( component_id = 'success-payload-scatter-chart' , component_property = 'figure' ),
              [ Entrée ( component_id = 'site-dropdown' , component_property = 'value' ),
              Entrée ( component_id = 'payload-slider' , component_property = 'value' )])
def  get_scatter_chart ( enter_site , charge utile ):
    faible , élevé  =  charge utile
     filtered_df =  spacex_df [( spacex_df [ 'Masse de la charge utile (kg)' ] > faible ) & ( spacex_df [ 'Masse de la charge utile (kg)' ] < élevé )]         
    si  enter_site  ==  'ALL' :
        figue  =  px . scatter ( filtered_df , x = 'Masse de la charge utile (kg)' , y = 'classe' ,
        color = 'Catégorie de la version Booster' ,
        title = 'Corrélation entre la charge utile et le succès pour tous les sites' )
        retour  figue
    sinon :
        figue  =  px . scatter ( filtered_df [ filtered_df [ 'Lancer le site' ] ==  enter_site ],
        x = 'masse de la charge utile (kg)' , y = 'classe' ,
        color = 'Catégorie de la version Booster' ,
        title = f'Corrélation entre la charge utile et le succès pour le site { enter_site } ' )
        retour  figue

# Exécutez l'application
si  __nom__  ==  '__main__' :
    application . run_server ()
