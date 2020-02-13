# -*- coding: utf-8 -*-
"""
Created on Wed Feb  5 19:54:21 2020
@author: esol
"""


from neqsim.thermo import *
from neqsim import java_gateway
from neqsim.thermo import WAT
neqsim = java_gateway.jvm.neqsim
neqsim.util.database.NeqSimDataBase.setConnectionString("jdbc:derby:C:/Users/MBUVA/Desktop/NTNU E.Solbra/neqsimthermodatabase");
neqsim.util.database.NeqSimDataBase.setCreateTemporaryTables(True);
    	

        
# Start by creating a fluid in neqsim
fluid1 = fluid("srk")  # create a fluid using the SRK-EoS
5
fluid1.addComponent("nitrogen", 0.48, "mol/sec")
fluid1.addComponent("CO2", 4.04, "mol/sec")
fluid1.addComponent("methane", 57.41, "mol/sec")
fluid1.addComponent("ethane", 9.28, "mol/sec")
fluid1.addComponent("propane", 5.62, "mol/sec")
fluid1.addComponent("i-butane", 1.00, "mol/sec")
fluid1.addComponent("n-butane", 2.22, "mol/sec")
fluid1.addComponent("i-pentane", 0.83, "mol/sec")
fluid1.addComponent("n-pentane", 1.05, "mol/sec")
fluid1.addComponent("n-hexane", 1.35, "mol/sec")
fluid1.addTBPfraction("C7", 2.21, 91.4/1000.0,0.739)
fluid1.addTBPfraction("C8", 2.59, 103.0/1000.0,0.771)
fluid1.addTBPfraction("C9", 1.49, 118.5/1000.0,0.785)
fluid1.addPlusFraction("C10", 10.43, 252.0 / 1000.0, 0.860);
fluid1.getCharacterization().characterisePlusFraction();
fluid1.getWaxModel().addTBPWax();
fluid1.createDatabase(True);
fluid1.setMixingRule(2);
fluid1.addSolidComplexPhase("wax");
fluid1.setMultiphaseWaxCheck(True)

fluid1.setTemperature(15.00, "C")
fluid1.setPressure(1.01, "bara")

TPflash(fluid1)
printFrame(fluid1)



waxTemp = WAT(fluid1)-273.15
print("WAT ", waxTemp, " °C")
