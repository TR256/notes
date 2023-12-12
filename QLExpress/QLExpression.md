```java
ExpressRunner runner = new ExpressRunner();
runner.addOperatorWithAlias("如果", "if", null);
runner.addOperatorWithAlias("则", "then", null);
runner.addOperatorWithAlias("否则", "else", null);
DefaultContext<String, Object> context = new DefaultContext<>();
long duration = 3600L * 4;
context.put("评审用时", duration / 3600D);
String express = "if (评审用时 >= 0 && 评审用时 <= 2.0 ) { return 评审用时 * 600.00; } return 1200.00 + (评审用时 - 2) * 300.00; ";
Object expressValue = runner.execute(express, context, null, true, true);
BigDecimal result = new BigDecimal(String.valueOf(expressValue));
System.out.println(result.setScale(2, RoundingMode.HALF_UP));
String expression = "如果(评审用时 <= 0) 则 { return 0.00; } 否则 { 如果(评审用时 <= 2.0) 则 { return 1200.00; } 否则 { 如果(评审用时 <= 4.5) 则 { return 1200.00 + (评审用时 - 2.0) * 400.00; } 否则 { return 3000.00; } } }";
Object expressionValue = runner.execute(expression, context, null, true, true);
BigDecimal expressionResult = new BigDecimal(String.valueOf(expressionValue));
System.out.println(expressionResult.setScale(2, RoundingMode.HALF_UP));

//////////////////////////////////////////
//    如果( 评审用时 <= 0 ) 则 {
//        return 0.00;
//    } 否则 {
//        如果( 评审用时 <= 2.0 ) 则 {
//            return 1200.00;
//        } 否则 {
//            如果( 评审用时 <= 4.5 ) 则 {
//                return 1200.00 + (评审用时 - 2.0) * 400.00;
//            } 否则 {
//                return 3000.00;
//            }
//        }
//    }
/////////////////////////
//if( 评审用时 <= 0.0 ){
//    return 0.00;
//}else if ( 评审用时 <= 2.0 ) {
//    return 1200.00;
//}else if(评审用时 <= 4.5){
//    return 1200.00 + (评审用时 - 2.0 ) * 400;
//} else{
//    return 3000.00;
//}
//////////////////////////
```
