# 2021 年 0222 题库版本 SQL 文件

* 分享读取文件源码分享
  * 简单处理响应，并返回json格式。

```php
public static function examFileToJson(Request $request){
  //读取请求的参数
  $content = $request->input("content");
  $singleLine = explode("\n",$content);
  $tempTotal = [];
  foreach($singleLine as $line){
    $s = str_replace(["[","]"],["",""], $line);
    if($s == ""){
      continue;
    }
    $tempTotal[] = $s;
  }
  //固定格式检查
  if( count($tempTotal) %7 != 0 ){
    return;
  }
  $all = [];
  //批次处理
  for( $i = 1; $i <= count($tempTotal) / 7; $i++){
    $temp = [];
    for( $j=($i-1)*7 ; $j<($i-1)*7+7 ; $j++){
      $data = $tempTotal[$j];
      //取出每行首字
      $firstWord = mb_substr($data, 0, 1);
      switch($firstWord){
        case "I":
          $temp["I"] = mb_substr($data, 1);
          break;
        case "Q":
          $temp["Q"] = mb_substr($data, 1);
          break;
        case "A":
          $temp["A"] = mb_substr($data, 1);
          break;
        case "B":
          $temp["B"] = mb_substr($data, 1);
          break;
        case "C":
          $temp["C"] = mb_substr($data, 1);
          break;
        case "D":
          $temp["D"] = mb_substr($data, 1);
          break;
        case "P":
          $temp["P"] = mb_substr($data, 1);
          break;
      }
    }
    $all[] = $temp;
  }
  return var_dump($all);
}
```