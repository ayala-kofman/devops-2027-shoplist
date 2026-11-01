image אחד 
container שתי
9001 shalom
9002 Hello
כדי למנוע התנגשיות בין הפורטים במחשב 
אבל בתוך ה container אותו ה dockerfile יודע לנווט אותו בהתאם
מוסיפים תחת services שירות בשם greeter-fr, משתנה סביבה GREETING: Bonjour ומיפוי פורטים "9003:8000".
כדי לשמור את הנתונים גם לאחר מחיקת הקונטיינר ויצירתו מחדש צריך volume ולכן ב postgres נשתמש בו
אבל greeter לא שומר נתונים כלל אלא רק מדפיס ולכן לא צריך volume
