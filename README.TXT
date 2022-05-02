This repository contains a version of the code required to introduce a CO2 tax in the standard functions of GenX.

The changes have been marked with a "NEW_CO2_TAX" comment before them, to make it easier to find them in the code.

The main changes are the following:

In the settings file for the scenario, it is now allowed to have CO2cap==4. When this is the case, the code will read the desired CO2 tax (as described below) and apply it consistently for every generator and every time step in the simulation.

The Load_fuels module now reads (when the appropriate CO2cap==4 setting is used) the CO2 tax from cell A2 of Fuels_data.csv (the example given is for an 80 USD/ton). The CO2 tax must be expressed as USD per ton of CO2. If CO2cap!=4, the CO2 tax is set at 0 for the subsequent steps. The CO2 Tax scalar is stored under the entry "CO2_Tax_per_Ton" in the inputs dictionary.

The Load_generators module now creates a new column with the CO2_Tax_per_MWh. To do so, the parameter already calculated in the code CO2_per_MWh is simply multiplied
by the CO2 tax. A similar procedure applies for the CO2 tax cost of start-ups. These are added to the C_Start column in this step too.

The CO2_Tax_per_MWh is added to the variable costs of the discharge module. There is no need to change anything in the ucommit module because, as mentioned, the C_Start
costs will already reflect the CO2 tax cost of start-ups (plus the fuel costs plus the fixed costs).

Finally, the costs of the CO2 tax are written in the NetRevenue.csv file. There are other output files where the information would be interesting, however.

