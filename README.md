# DynamicNumber
DynamicNumber - is a simple java class for performing Number operations on different accuracy modes (Double mode, BigDecimal mode, BigFraction mode)

It has 3 modes:  
1. Double mode - in this mode all operations will be performed using double numbers
2. BigDecimal mode - in this mode all operations will be performed using BigDecimal number class
3. BigFraction mode - in this mode all operations will be performed using BigFraction number class from apache commons math library.  

Default mode is double. 

Modes BigDecimal and BigFraction are usually used for division operations of very high accuracy or for operations on large numbers(when double is not enough). BigFraction is the most accurate and it gives no precision loss in division operations. It should be noted that, that the higher accuracy is the lesser performance we get. So you should use different modes based on your requirements. 

Mode is defined using <i>DynamicNumber.modeDefault = DynamicNumber.modeBigDecimal;</i> or passing required mode when initiating object.

DynamicNumber class also has function factorial that uses BigInteger class to calculate factorial for large integers when double accuracy is not enough. 

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
        
        
Let's say we want to calculate <i>(1/7 * 1/3) / (1/9) and repeat 5 times</i> and compare results:  

        DynamicNumber a = DynamicNumber.ONE().div(7);  
        DynamicNumber b = DynamicNumber.ONE().div(3);  
        DynamicNumber c = DynamicNumber.ONE().div(9);  
        
        DynamicNumber.modeDefault = DynamicNumber.modeBigDecimal;  
        DynamicNumber.rm = RoundingMode.HALF_UP; //this is default value  
        DynamicNumber.sc = 40; //sc is for scale that defines precision for BigDecimal class, default is 40  
        DynamicNumber a1 = DynamicNumber.ONE().div(7);  
        DynamicNumber b1 = DynamicNumber.ONE().div(3);  
        DynamicNumber c1 = DynamicNumber.ONE().div(9);  
        
        DynamicNumber.modeDefault = DynamicNumber.modeBigFraction;  
        DynamicNumber a2 = DynamicNumber.ONE().div(7);  
        DynamicNumber b2 = DynamicNumber.ONE().div(3);  
        DynamicNumber c2 = DynamicNumber.ONE().div(9);  
        
        for (int i = 0; i < 5; i++) {   
            a = a.mult(b).div(c).pow(3);  
            a1 = a1.mult(b1).div(c1).pow(3);  
            a2 = a2.mult(b2).div(c2).pow(3);  
        }  
        
        System.out.println("Double mode: "+a);  
        System.out.println("BigDecimal mode: " +a1.doubleValue());  
        System.out.println("BigFraction mode: " +a2.doubleValue());    
        
The output will be:

Double mode: 6.857909343637325E-33  
BigDecimal mode: 6.857909343637392E-33  
BigFraction mode: 6.857909343637393E-33    

As seen above we get some minor deviations due to precision loss while intermediary divisions, which could be important in precision required calculations. 

One good example for this class is that, we could implement Gaussian elemination algorithm using BigFraction mode that will give exact solutions for any linear system. 

PS: Please also download Apache Commons Math library in order to use BigFraction class. Version used in project is 3.6.1 located in lib folder. Link for the latest version: http://commons.apache.org/proper/commons-math/download_math.cgi


