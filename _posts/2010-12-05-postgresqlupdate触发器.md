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
 postgresql 触发器: CREATE OR REPLACE FUNCTION updateinfo() RETURNS &#8221;trigger&#8221; AS $BODY$ DECLARE detltanmoney  integer; deltangiftmoney  integer; deltarmb  integer; Begin detltanmoney= NEW.nmoney-OLD.nmoney; deltangiftmoney= NEW.ngiftmoney-OLD.ngiftmoney; deltarmb= NEW.nrmb-OLD.nrmb; INSERT INTO tb\_user\_account\_changelog( id,n\_deltamoney, n\_deltagiftmoney, n\_deltarmb, nbookid, dtime) VALUES (NEW.id, detltanmoney, deltangiftmoney, deltarmb, 1, now()); RETURN NULL; END; $BODY$ LANGUAGE &#8217;plpgsql&#8217; VOLATILE; ALTER FUNCTION updatetbuseraccount() OWNER TO armory; CREATE TRIGGER tb\_user\_account_changelog AFTER UPDATE ON tbuseraccount FOR EACH ROW EXECUTE PROCEDURE updatetbuseraccount () ;