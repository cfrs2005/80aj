---
title: 121122 光线(Gxcms)采集中断 可能原因至于 imagecreatefrombmp
layout: post
permalink: /2478.html
categories:
  - Code
tags:
  - gd
  - gxcms
  - imagecreatefrombmp
  - 中断
  - 采集
  - 重绘
---
首先祝 各位还在深夜忙碌的博友 感恩节快乐，吃鸡了木有，反正我是木有， 好吧 明天也算是感恩节2天中的一天，所以 回家和老婆孩子好好聚聚.

**PS 关于 感恩节:**

<pre>感恩节（Thanksgiving Day）是美国和加拿大共有的节日，由美国人民独创，原意是为了感谢上天赐予的好收成、感谢印第安人的帮助。在美国，自1941年起，感恩节是在每年11月的第四个星期四，并从这一天起将休假两天,而加拿大与美国的感恩节时间不同，10月第二个星期一。像中国的春节一样，在这一天，成千上万的人们不管多忙，都要和自己的家人团聚。加拿大的感恩节则起始于1879年，是在每年10月第二个星期一，与美国的哥伦布日相同。
</pre>

更多资料点击查看 <a href="http://zh.wikipedia.org/zh/%E6%84%9F%E6%81%A9%E8%8A%82" target="_blank">感恩节</a>

最近写的 gxcms 自动采集 今天发生了个奇怪的事 采集的时候，只采集了1部分 然后中断 就去生成网页了， 晚上回家仔细看了下代码 原来问题出在：

<pre lang="php">Fatal error: Call to undefined function imagecreatefrombmp

</pre>

<span style="color: #ff0000;"><strong>php gd库 本身是不存在 imagecreatefrombmp 的 , 虽然有 imagecreatefromwbmp , 但是 Gxcms 在使用gd 重绘的时候 用了 抓去图片的 头部信息去 做类型判断 然后填充 选择 函数 。</strong></span>

<span style="color: #ff0000;">有些图片 后缀虽然是 jpg 把图片 后缀 从bmp 改成 jpg 虽然在上传初期检查后缀过关了 ， 但是 实际上 因为图片本身信息没有改变 依然还是BMP 所以在PHP 抓去成功后 重绘获取到图片信息 内容里面的额 type 依然是 bmp</span>

废话多了 解决办法：

<pre lang="php">// 站点目录  /core/ThinkPHP/Lib/ORG/Util/Image.class.php  530行增加下面内容即可 
         if($sInfo['type']){
			$sInfo['type']='jpeg';
		}
        //建立图像
        $sCreateFun="imagecreatefrom".$sInfo['type'];
        $sImage=$sCreateFun($source);
        $wCreateFun="imagecreatefrom".$wInfo['type'];

</pre>

当然网上也有代码 不过我没试过 有兴趣的同学可以试试。 好像意义不大：

<pre lang="php">function imagecreatefrombmp($file)
{
        global  $CurrentBit, $echoMode;
        $f=fopen($file,"r");
        $Header=fread($f,2);

        if($Header=="BM")
        {
                $Size=freaddword($f);
                $Reserved1=freadword($f);
                $Reserved2=freadword($f);
                $FirstByteOfImage=freaddword($f);

                $SizeBITMAPINFOHEADER=freaddword($f);
                $Width=freaddword($f);
                $Height=freaddword($f);
                $biPlanes=freadword($f);
                $biBitCount=freadword($f);
                $RLECompression=freaddword($f);
                $WidthxHeight=freaddword($f);
                $biXPelsPerMeter=freaddword($f);
                $biYPelsPerMeter=freaddword($f);
                $NumberOfPalettesUsed=freaddword($f);
                $NumberOfImportantColors=freaddword($f);

                if($biBitCount&lt;24)
                {
                        $img=imagecreate($Width,$Height);
                        $Colors=pow(2,$biBitCount);
                        for($p=0;$p&lt;$Colors;$p++)
                        {
                                $B=freadbyte($f);
                                $G=freadbyte($f);
                                $R=freadbyte($f);
                                $Reserved=freadbyte($f);
                                $Palette[]=imagecolorallocate($img,$R,$G,$B);
                        }

 


                        if($RLECompression==0)
                        {
                                $Zbytek=(4-ceil(($Width/(8/$biBitCount)))%4)%4;

                                for($y=$Height-1;$y>=0;$y--)
                                {
                                        $CurrentBit=0;
                                        for($x=0;$x&lt;$Width;$x++)
                                        {
                                                $C=freadbits($f,$biBitCount);
                                                imagesetpixel($img,$x,$y,$Palette[$C]);
                                        }
                                        if($CurrentBit!=0) {freadbyte($f);}
                                        for($g=0;$g&lt;$Zbytek;$g++)
                                        freadbyte($f);
                                }

                        }
                }


                if($RLECompression==1) //$BI_RLE8
                {
                        $y=$Height;

                        $pocetb=0;

                        while(true)
                        {
                                $y--;
                                $prefix=freadbyte($f);
                                $suffix=freadbyte($f);
                                $pocetb+=2;

                                $echoit=false;

                                if($echoit)echo "Prefix: $prefix Suffix: $suffix<BR />";
                                if(($prefix==0)and($suffix==1)) break;
                                if(feof($f)) break;

                                while(!(($prefix==0)and($suffix==0)))
                                {
                                        if($prefix==0)
                                        {
                                                $pocet=$suffix;
                                                $Data.=fread($f,$pocet);
                                                $pocetb+=$pocet;
                                                if($pocetb%2==1) {freadbyte($f); $pocetb++;}
                                        }
                                        if($prefix>0)
                                        {
                                                $pocet=$prefix;
                                                for($r=0;$r&lt;$pocet;$r++)
                                                $Data.=chr($suffix);
                                        }
                                        $prefix=freadbyte($f);
                                        $suffix=freadbyte($f);
                                        $pocetb+=2;
                                        if($echoit) echo "Prefix: $prefix Suffix: $suffix<BR />";
                                }

                                for($x=0;$x&lt;strlen($Data);$x++)
                                {
                                        imagesetpixel($img,$x,$y,$Palette[ord($Data[$x])]);
                                }
                                $Data="";

                        }

                }


                if($RLECompression==2) //$BI_RLE4
                {
                        $y=$Height;
                        $pocetb=0;

                        /*while(!feof($f))
                        echo freadbyte($f)."_".freadbyte($f)."<BR />";*/
                        while(true)
                        {
                                //break;
                                $y--;
                                $prefix=freadbyte($f);
                                $suffix=freadbyte($f);
                                $pocetb+=2;

                                $echoit=false;

                                if($echoit)echo "Prefix: $prefix Suffix: $suffix<BR />";
                                if(($prefix==0)and($suffix==1)) break;
                                if(feof($f)) break;

                                while(!(($prefix==0)and($suffix==0)))
                                {
                                        if($prefix==0)
                                        {
                                                $pocet=$suffix;

                                                $CurrentBit=0;
                                                for($h=0;$h&lt;$pocet;$h++)
                                                $Data.=chr(freadbits($f,4));
                                                if($CurrentBit!=0) freadbits($f,4);
                                                $pocetb+=ceil(($pocet/2));
                                                if($pocetb%2==1) {freadbyte($f); $pocetb++;}
                                        }
                                        if($prefix>0)
                                        {
                                                $pocet=$prefix;
                                                $i=0;
                                                for($r=0;$r&lt;$pocet;$r++)
                                                {
                                                        if($i%2==0)
                                                        {
                                                                $Data.=chr($suffix%16);
                                                        }
                                                        else
                                                        {
                                                                $Data.=chr(floor($suffix/16));
                                                        }
                                                        $i++;
                                                }
                                        }
                                        $prefix=freadbyte($f);
                                        $suffix=freadbyte($f);
                                        $pocetb+=2;
                                        if($echoit) echo "Prefix: $prefix Suffix: $suffix<BR />";
                                }

                                for($x=0;$x&lt;strlen($Data);$x++)
                                {
                                        imagesetpixel($img,$x,$y,$Palette[ord($Data[$x])]);
                                }
                                $Data="";

                        }

                }


                if($biBitCount==24)
                {
                        $img=imagecreatetruecolor($Width,$Height);
                        $Zbytek=$Width%4;

                        for($y=$Height-1;$y>=0;$y--)
                        {
                                for($x=0;$x&lt;$Width;$x++)
                                {
                                        $B=freadbyte($f);
                                        $G=freadbyte($f);
                                        $R=freadbyte($f);
                                        $color=imagecolorexact($img,$R,$G,$B);
                                        if($color==-1) $color=imagecolorallocate($img,$R,$G,$B);
                                        imagesetpixel($img,$x,$y,$color);
                                }
                                for($z=0;$z&lt;$Zbytek;$z++)
                                freadbyte($f);
                        }
                }
                return $img;

        }


        fclose($f);


}

function freadbyte($f)
{
        return ord(fread($f,1));
}

function freadword($f)
{
        $b1=freadbyte($f);
        $b2=freadbyte($f);
        return $b2*256+$b1;
}

function freaddword($f)
{
        $b1=freadword($f);
        $b2=freadword($f);
        return $b2*65536+$b1;
}
</pre>