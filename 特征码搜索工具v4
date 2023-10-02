var html = '<div id="asopage" style="background-color: #FDFDFD; width:99.5%; height:99.5%; position:absolute; left:0; top:0; border:1px solid #B8B8B880; border-radius: 5px; padding: 0px; z-index: 99999;-webkit-touch-callout: default;">特征码扫描工具v4<br/><button onclick="firstFuck()">首次扫描</button><button onclick="reFuck()">筛选</button><button onclick="outputText()">JSON转文本</button><br/><div id="tips"></div><div id="content" class="scrollbar" style="max-height:78%; width:100%; -webkit-user-select: all; border-radius: 2.5px"></div></div>';

$(document).ready(function() {
  $('body').append(html);
});
function firstFuck() {
  // 获取用户输入的16进制地址
  inputAddress = prompt("请输入16进制地址：");
  // 将用户输入的16进制地址转换为整数
  address = parseInt(inputAddress, 16);
  // 获取用户输入的最大偏移量
  inputMaxOffset = prompt("请输入最大偏移量：");
  // 将用户输入的最大偏移量转换为整数
  maxOffset = parseInt(inputMaxOffset, 16);
  // 获取用户输入的数据类型
  dataType = prompt("请输入数据类型：");
  // 存储第一次扫描结果的数组
  firstScanResults = [];
  // 执行第一次扫描
  scanValues(address - maxOffset, address + maxOffset, firstScanResults);
  var firstScanResultsJson = JSON.stringify(firstScanResults);
  $("#tips").text("共采取到" + firstScanResults.length + "条结果");
  $("#content").text(firstScanResultsJson);
}

function reFuck() {
  // 获取用户输入的16进制地址
  inputAddress = prompt("请输入16进制地址：");
  // 将用户输入的16进制地址转换为整数
  address = parseInt(inputAddress, 16);
  // 获取用户输入的最大偏移量
  inputMaxOffset = prompt("请输入最大偏移量：");
  // 将用户输入的最大偏移量转换为整数
  maxOffset = parseInt(inputMaxOffset, 16);
  // 获取用户输入的数据类型
  dataType = prompt("请输入数据类型：");
  // 存储第一次扫描结果的数组
  var inputJson = prompt("请输入JSON：");
  firstScanResults = JSON.parse(inputJson);
  secondScanResults = [];

  scanValues(address - maxOffset, address + maxOffset, secondScanResults);

  var matchedResults = [];
  for (var i = 0; i < firstScanResults.length; i++) {
    for (var j = 0; j < secondScanResults.length; j++) {
      if (
        firstScanResults[i].offset === secondScanResults[j].offset &&
        firstScanResults[i].value === secondScanResults[j].value
      ) {
        matchedResults.push({
          offset: firstScanResults[i].offset,
          value: firstScanResults[i].value,
        });
        break;
      }
    }
  }

  var matchedResultsJson = JSON.stringify(matchedResults);
  $("#tips").text("共筛选到" + matchedResults.length + "条结果");
  $("#content").text(matchedResultsJson);
}

// 扫描指定范围内的值
function scanValues(startAddress, endAddress, resultsArray) {
  for (var i = startAddress; i <= endAddress; i += 4) {
    // 使用h5gg.getValue函数获取地址i处的值
    var value = h5gg.getValue("0x" + i.toString(16), dataType);
    // 计算当前地址与输入地址的偏移量
    var offset = i - address;
    // 将结果存储在resultsArray数组中
    resultsArray.push({ offset: offset, value: value });
  }
}

function outputText() {
  var inputJson = $("#content").text();
  var matchedResults = JSON.parse(inputJson);
  var output = "";
  var validCount = 0; // 记录有效结果的数量
  // 构建输出结果的字符串
  for (var i = 0; i < matchedResults.length; i++) {
    var result = matchedResults[i];
    if (result.value == 0) {
      continue;
    }
    var offset =
      result.offset >= 0 ? "0x" + result.offset.toString(16) : "-0x" + Math.abs(result.offset).toString(16);
    output += "[" + validCount + "]" + "Offset:" + offset + " Value:" + result.value + "<br>";
    validCount++; // 增加有效结果的数量，也作为有效结果的序号
  }
  // 弹窗输出结果
  $("#content").html(output);
  $("#tips").text("共找到" + matchedResults.length + "条特征码 除去0后剩" + validCount + "条");
}
