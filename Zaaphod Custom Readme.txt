This branch is for customizing smoothieware for my machines.

Planned changes:

Come up with some method to control a second Z Axis.  
    Summary:
        Most of my machines in the field have 2 Z axis, I need a way to control the second Z axis.
    The solution must meet the following criteria:
        Must be able to home the second Z
        Second Z must be stopped by limit switches
        Spindle commands must affect second Z when activated
        Physical offset must be compensated for when second Z is activated
        An accepted command must be used to switch to the second Z head in case this feature is to be used by others
        It would be nice if the solution could be expanded to more than 2 Z Axis.

Modify Home procedure.
    Summary:
        Beseides adjustments for the above multiple Z axis, most of my machines are very large, and 
        home procedure can take a long time. I also have many customers who run the same program on
        multiple machines, and they would benefit from some settings being able to be set independatly
        on each machine.
    The solution must meet the following criteria:
        Perform home in the fastest way practical while maintianing accuracy
        Move to origin after home using preset rapid rates, not fast home rates
            The fast home rates are the fastest rate you can hit a switch without completly using it's travel distance 
            This is much much slower than the rapid rates of the machine.  Machines with large tables take very long
            to move to origin at the fast home rate, so using the default rapid rate is prefered
        Move to park after home
            On many machines it is benefecial to move to some point other than 0,0 after home
        Reset rapid rates to default after home
            Since some hosts change the G0 feedrate with F commands, it's benefecial for the home procedure to leave 
            the mahcine in a known state which includes a known G0 feedrate
        Create a command to reset the rapid rate without homing
            There are times the rapid rate could be changed for G0 feedrate, but then you want a quick way to reset it 
            back to default.  These defaults can be different on different machines so the best solution is on which 
            does not require a hard coded feedrate in a program.
