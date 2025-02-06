# **Data Protection and Auditability**

## **Comprehensive Data Protection and Privacy**
Amazon Bedrock ensures **data privacy and security** through the following measures:
- **Data Isolation:** Your data **is not** used for **service improvement** and **is not shared** with third-party model providers.
- **AWS PrivateLink Integration:** Allows private connectivity between **foundation models (FMs)** and your **virtual private cloud (VPC)** without exposing traffic to the internet.
- **Encryption:**  
  - **In Transit & At Rest:** Data is encrypted at all stages.  
  - **Customization Privacy:** Customized FMs are trained on a **separate copy** of the base model, ensuring your **original data remains private**.

---

## **Secure your Generative AI Applications**
To **secure custom FMs**, Amazon Bedrock provides **defense-in-depth strategies**:
- **AWS Key Management Service (AWS KMS):** Encrypts stored **customized FMs**.
- **AWS Identity and Access Management (IAM):**  
  - Controls **who** can access **specific FMs**.  
  - Defines which **services** can perform inferences.  
  - Restricts **console access** to authorized users.

### **🔹 FM Protection Using IAM & AWS KMS**
AWS IAM and AWS KMS work together to ensure **strict access control** and **encryption** for enhanced security.

---

## **Support for Governance & Auditability**
Amazon Bedrock provides **logging and monitoring** tools to meet governance and audit requirements:
- **Amazon CloudWatch:**  
  - **Tracks usage metrics** for audits.  
  - Allows **customized dashboards** for monitoring system performance.
- **AWS CloudTrail:**  
  - **Monitors API activity** and system interactions.  
  - Helps **troubleshoot issues** when integrating external systems into generative AI applications.

---

## **Conclusion**
Amazon Bedrock prioritizes **security, privacy, and compliance** by ensuring **data protection**, **private model customization**, **strict access control**, and **comprehensive monitoring**. This makes it a **trustworthy** and **governance-compliant** platform for building generative AI applications.