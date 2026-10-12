# Garba Photo Portal (Starter Project)

## क्या करता है
- Admin password के साथ bulk event-photo upload
- Private S3 storage में original + thumbnail
- Amazon Rekognition collection में faces index
- Visitor selfie upload करके matching photos खोज सकता है
- Razorpay order ₹2 का बनता है
- Server payment signature verify करने के बाद 2 मिनट का signed download link देता है

## चलाने के लिए
1. Node.js 20+ install करें।
2. इस folder में terminal खोलें और `npm install` चलाएँ।
3. `.env.example` की copy `.env` नाम से बनाकर values भरें।
4. AWS S3 bucket बनाएँ और AWS Rekognition collection बनाएं (या IAM user को collection create करने की permission दें)।
5. AWS credentials को `.env` में रखें या hosting environment में IAM role इस्तेमाल करें।
6. Razorpay account में API keys लें और `.env` में डालें।
7. `npm start` चलाएँ; browser में `http://localhost:3000` खोलें।

## AWS permissions
Runtime role/user को S3 bucket पर `s3:PutObject`, `s3:GetObject` और Rekognition पर `rekognition:CreateCollection`, `rekognition:IndexFaces`, `rekognition:SearchFacesByImage` permissions चाहिए। Production में minimum permissions दें।

## जरूरी बातें
- यह starter project है, live public website नहीं; hosting, credentials और deployment configure करना बाकी है।
- Payment signature verification implemented है, लेकिन production launch से पहले Razorpay payment status को API से fetch करके captured/paid status verify करें और order/photo association server-side persist करें। इसे live करने से पहले webhook + durable database जोड़ना उचित है।
- Local JSON file serverless hosting पर persistent नहीं होती; production में PostgreSQL/Supabase जैसे database से बदलें।
- Group photos में Rekognition हर detected face index करता है; search result photo ID से map होता है।
- Face data sensitive हो सकता है। Upload करने से पहले event attendees को clear notice दें, appropriate consent लें, retention/deletion policy रखें, और लागू privacy laws का पालन करें।
- ₹2 payment पर gateway fees/taxes के कारण net receipt ₹2 से कम हो सकती है; current fee schedule verify करें।
