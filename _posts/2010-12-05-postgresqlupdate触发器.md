---
title: 101205 postgresql update 触发器
layout: post
permalink: /1583.html
categories:
  - DataBase
tags:
  - POSTGRESQL
  - 触发器
---
[<img class="aligncenter size-medium wp-image-1427" title="php" src="http://www.80aj.com/wp-content/uploads/2010/08/php-300x190.jpg" alt="" width="300" height="190" />][1]

postgresql 触发器:

> CREATE OR REPLACE FUNCTION updateinfo()
> 
> RETURNS &#8221;trigger&#8221; AS
> 
> $BODY$
> 
> DECLARE
> 
> detltanmoney  integer;
> 
> deltangiftmoney  integer;
> 
> deltarmb  integer;
> 
> Begin
> 
> detltanmoney= NEW.nmoney-OLD.nmoney;
> 
> deltangiftmoney= NEW.ngiftmoney-OLD.ngiftmoney;
> 
> deltarmb= NEW.nrmb-OLD.nrmb;
> 
> INSERT INTO tb\_user\_account_changelog(
> 
> id,n\_deltamoney, n\_deltagiftmoney, n_deltarmb,
> 
> nbookid, dtime)
> 
> VALUES (NEW.id, detltanmoney, deltangiftmoney, deltarmb,
> 
> 1, now());
> 
> RETURN NULL;
> 
> END;
> 
> $BODY$
> 
> LANGUAGE &#8217;plpgsql&#8217; VOLATILE;
> 
> ALTER FUNCTION updatetbuseraccount() OWNER TO armory;
> 
> CREATE TRIGGER tb\_user\_account_changelog
> 
> AFTER UPDATE ON tbuseraccount
> 
> FOR EACH ROW EXECUTE PROCEDURE updatetbuseraccount ()
> 
> ;

 [1]: http://www.80aj.com/wp-content/uploads/2010/08/php.jpg