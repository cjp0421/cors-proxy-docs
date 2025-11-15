# Documentation Outline

## 1. Overview
- What problem the guide solves  
- When this pattern is useful  
- High-level summary of steps  
- Who the guide is for  

---

## 2. Understanding CORS
- Short explanation of CORS  
- Why browsers block certain external API calls  
- Why public APIs often trigger CORS  
- Why a proxy server solves the issue  
- Simple mental model: frontend → Lambda → public API → response  

---

## 3. Architecture Overview
- High-level request flow description  
- Role of the Lambda function  
- Role of API Gateway  
- Why secrets should live in Lambda (not frontend code)  

---

## 4. Before You Begin (Prerequisites)
- AWS account  
- Basic Go setup  
- Basic knowledge of making API calls  
- Frontend setup context (e.g., Vite, React)  

---

## 5. Create the Lambda (Click-Ops)
- Navigate to AWS Lambda in the console  
- Create function (Go runtime)  
- Add environment variables (API key)  
- Set basic permissions  
- Save and deploy  

---

## 6. Go Handler Overview
- What the handler needs to do conceptually:  
  - Receive event  
  - Call upstream API  
  - Use environment variable for secret  
  - Format response  
  - Add CORS headers  
  - Return JSON  

---

## 7. Connect Lambda to API Gateway
- Create an HTTP API  
- Add integration to the Lambda  
- Deploy a stage  
- Copy the invoke URL  

---

## 8. Test the Proxy
- Test using curl  
- Test using browser  
- Expected response examples  
- Debugging common errors  

---

## 9. Security & Abuse Considerations
- Lambda endpoint is technically public  
- API key must remain in Lambda environment variables  
- Use throttling on API Gateway  
- Add AWS Budget alerts for cost protection  
- Safe for demos, prototypes, and small apps  
- Notes on strengthening security for production  

---

## 10. Integrate With Your Frontend
- Swap direct API call with Lambda endpoint  
- Example `fetch()` call  
- What changes for the frontend developer  

---

## 11. Project Structure (Hugo)
- How the documentation pages are organized  
- Brief explanation of the content directory  
- How to run the Hugo site locally (`hugo server -D`)  
- Note that the site can be deployed to GitHub Pages

---

## 12. Appendix
- Glossary of terms  
- Complete example handler code  
- Extra troubleshooting notes (as needed)
- Additional diagrams (as needed)
