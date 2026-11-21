
shoplist-frontend:single | 92.8MB
shoplist-frontend:multi | 92.7MB
shoplist-frontend:kitchen | 244MB

##תשובות
#1
הדפדפן לא מדבר בכלל עם ה backend רק ה stats
הדפדפן שולח בקשה ל Nginx והוא מפנה את הבקשה ל backend
#2
כאשר האפלקציה יורדת שניה קודם הנתונים נשמרים ב postgres-data
ובכל פעם שהאפליקציה עולה שוב היא טוענת את הנתונים משם-כלום לא נמחק
אבל dowm-v מוחק לגמרי הכל כולל הdata ואז באמת הנתונים לא ישמרו כלל
#3
init.sql רץ פעם אחת בלבד רק בהפעלה הראשונה אז גם אם ישנו אותו זה לא ישפיע
הפקודה dowm -v ואח"כ up תגרום לקובץ לרוץ שוב וכאן השינוים כן ישפיעו  
#4
NETWORK ID     NAME             DRIVER    SCOPE
76d4077baa3c   bridge           bridge    local
839a9d4ab1b1   docker_default   bridge    local
2becb4931ecb   host             host      local
170c4d825b76   none             null      local

DRIVER    VOLUME NAME
local     docker_postgres-data

הרשת:docker_default
volume:docker_postgres-data
#5
image:Nginx,nginx.conf,dist-תקיה
cmd מגיע אוטומטית מ Nginx
multi-stage צריך בשלבי הבניה בלבד
#6
שתיהם מבוססים על אותו nginx
וןלכן משקלם כמעט זהה ההבדל הוא בגלל קבצים קטנים שמתוספים
#7
שניהם מתאימים לבקשה אבל Nginx בוחר את הארוך יותר
/api-מוריד את זה מהניתוב כדי שהבקשה תבוא לbackend
ללא  זה ותתאים כי אין ניתוב /api/products