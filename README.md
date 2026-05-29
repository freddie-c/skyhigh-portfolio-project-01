# skyhigh-portfolio-project-01

<img width="1437" height="808" alt="image" src="https://github.com/user-attachments/assets/d78a829d-b65c-4701-a349-49d13229f8c3" />

# SkyHigh Portfolio Project 1 — Static Website on AWS

My personal portfolio website, deployed on AWS using S3 for storage
and CloudFront for HTTPS + global delivery.

**Live URL:** https://d29d1z8rt8o192.cloudfront.net

Building a static website (HTML + CSS), hosted on Amazon S3,
served through AWS CloudFront with HTTPS, accessible from
anywhere in the world.

---

## Architecture

<img width="753" height="565" alt="image" src="https://github.com/user-attachments/assets/1d805df2-389f-497c-aab1-669ff1cb8ac2" />

User → CloudFront (HTTPS + CDN) → S3 Bucket (index.html + style.css)

---

## Tech Stack

- HTML5
- CSS3
- AWS S3 — static website hosting
- AWS CloudFront — HTTPS and global CDN
- AWS IAM — bucket policy for public read access
- Git & GitHub — version control and source storage

---

## What I Built

- Personal portfolio site with Header, About, Skills, Projects,
  and Contact sections
- S3 bucket configured for static website hosting
- CloudFront distribution with HTTPS enforced
- Public bucket policy granting s3:GetObject to everyone

---

## Deployment Steps

1. Created S3 bucket named `fred-cloud-portfolio-site` with
   static website hosting enabled
2. Disabled Block Public Access and added bucket policy to allow
   public reads
3. Uploaded `index.html` and `style.css` to the bucket
4. Created a CloudFront distribution pointing at the S3 website
   endpoint with HTTP → HTTPS redirect
5. Waited ~15 min for distribution to deploy, then verified
   the live URL loaded correctly

---

## Challenges & Solutions

**Block Public Access was still on after setting the bucket policy**
The bucket policy wasn't taking effect and the site was returning
403 errors. Turned out Block Public Access was overriding the policy
at the bucket level. Had to go into Permissions, uncheck Block All
Public Access, type "confirm," and save before the policy activated.

**"Make Public Using ACL" was greyed out**
ACL permissions were disabled by default on the bucket. Had to go
into Object Ownership settings and enable ACLs before the option
became available. Ended up using a bucket policy instead, which
is the cleaner approach anyway.

---

## What I'd Do Differently in Production

For a production deployment I would register a custom domain via
Route 53, attach an ACM certificate for a proper SSL cert instead
of the default CloudFront one, enable CloudFront access logging
to S3, and manage the entire infrastructure as code using Terraform 
so the setup is repeatable and version-controlled.

---

## Cost Note

Total monthly cost: $0.50, well within AWS Free Tier limits.
S3 storage and CloudFront data transfer at this scale are
essentially free for the first 12 months.

---

## Future Improvements

- Custom domain via Route 53 (e.g. fredrickculpepper.com)
- GitHub Actions CI/CD — auto-deploy on every git push
- CloudFront cache invalidation triggered on deploy
- ACM SSL certificate for custom domain HTTPS
