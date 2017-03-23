# DynamicNumber
DynamicNumber - is a simple java class for performing Number operations on different accuracy modes (double mode, BigDecimal mode, BigFraction mode)

It has 3 modes:  
1. Double mode - in this mode all operations will be performed using double numbers
2. BigDecimal mode - in this mode all operations will be performed using BigDecimal numbers
3. BigFraction mode - in this mode all operations will be performed using BigFraction number from apache commons math library.  

Default mode is double. 

Modes BigDecimal and BigFraction are usually used for division operation of very high accuracy. 

Example usages:  

        DynamicNumber t = new DynamicNumber(1/7);  
        t = new DynamicNumber(5.2);  
        t = new DynamicNumber(5,DynamicNumber.modeBigFraction);  
        t = DynamicNumber.ONE();  
        t = DynamicNumber.ZERO(DynamicNumber.modeBigDecimal);  
        t.doubleValue();  
        t.toString();  
        t.abs();  
        System.out.println(DynamicNumber.factorial(300));    
        
        
Let's say we want to calculate <i>(1/7 + (1/3)^5 - sqrt(1/9))/(1/7)</i> and compare results:  

        DynamicNumber a = DynamicNumber.ONE().div(7);  
        DynamicNumber b = DynamicNumber.ONE().div(3);  
        DynamicNumber c = DynamicNumber.ONE().div(9);  
        
        DynamicNumber.modeDefault = DynamicNumber.modeBigDecimal;  
        DynamicNumber a1 = DynamicNumber.ONE().div(7);   
        DynamicNumber b1 = DynamicNumber.ONE().div(3);  
        DynamicNumber c1 = DynamicNumber.ONE().div(9);  
        
        DynamicNumber.modeDefault = DynamicNumber.modeBigFraction;  
        DynamicNumber a2 = DynamicNumber.ONE().div(7);  
        DynamicNumber b2 = DynamicNumber.ONE().div(3);  
        DynamicNumber c2 = DynamicNumber.ONE().div(9);  
        
        System.out.println(a.add(b.pow(5)).sub(c.pow(0.5)).div(a));  
        System.out.println(a1.add(b1.pow(5)).sub(c1.pow(0.5)).div(a1));  
        System.out.println(a2.add(b2.pow(5)).sub(c2.pow(0.5)).div(a2) + ", Double value: " +a2.add(b2.pow(4)).sub(c2.pow(0.5)).div(a2).doubleValue());  
        
The output will be:

Double mode: -1.3045267489711934  
BigDecimal mode: -1.3045267489711932861118405427029303662135  
BigFraction mode: -5710564327505788361 / 4377498837804122112, Double value: -1.2469135802469133  

As seen above we get some deviations due to precision loss while intermediary divisions. 


