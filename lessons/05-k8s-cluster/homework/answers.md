רכיב	איפה רץ	מה עושה	אנלוגיה (בית חולים)
API server	הנהלה	הכניסה היחידה ל-cluster: מקבל ומאמת כל בקשה	דלפק הקבלה
etcd	הנהלה	מסד הנתונים של ה-cluster: מה רצוי ומה קיים	תיק המטופל
scheduler	הנהלה	בוחר לכל pod חדש על איזה node ירוץ	המאבחנת ששולחת מטופל לחדר פנוי
controller manager	הנהלה	משווה בלי הפסקה רצוי מול בפועל ומתקן	מנהלת המחלקה שבודקת שיש מספיק צוות
kubelet	כל node	מריצה את מה ששובץ ל-node ומדווחת שהוא חי	האחות האחראית במחלקה
container runtime	כל node	מריץ בפועל containers מ-images	ציוד הטיפול
kube-proxy	כל node	מנתב בקשות לשם של Service ל-pods הנכונים	המוקדנית שמעבירה שיחות לשלוחה הנכונה
coredns	pods ב-kube-system, רץ על ה-nodes	DNS פנימי: הופך שם של Service לכתובת	ספר הטלפונים הפנימי


///תרחישים
1. scale ל-4. kubectl שולח ל-API server, שרושם ב-etcd: רצויים 4. ה-controller manager רואה 2 מתוך 4 ויוצר 2 pods. ה-scheduler משבץ אותם ל-nodes, ו-kubelet מריצה אותם.

2. שלוש בלילה. container שקרס: kubelet מרימה אותו מחדש באותו pod. pod שנמחק: ה-controller manager רואה פחות מהרצוי ויוצר חדש, וה-scheduler משבץ אותו. הכול אוטומטי.

3. node נכבה. בענן: ההנהלה מסמנת את node 2 כ-NotReady, וה-pods נוצרים מחדש על node 1 ו-3. ב-Docker Desktop יש node אחד, אז אין לאן לעבור, והכול נעצר עד שהמחשב עולה שוב.

4. מהכיתה ל-EKS. imagePullPolicy: Never לא יעבוד, כי ל-nodes בענן אין את ה-image המקומי. צריך לדחוף אותו ל-registry ולעדכן את image:. ו-NodePort לא חושף לאינטרנט, אז מחליפים ל-LoadBalancer.

5. pod בודד. kubectl run יוצר pod בלי Deployment, ולכן אף אחד לא מחזיר אותו. כדי ש-stats יחזור תמיד, מריצים אותו דרך Deployment. 
