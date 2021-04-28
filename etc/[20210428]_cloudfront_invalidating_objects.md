# CloudFront 캐시 삭제 - 객체 무효화
- 당장 급하게 적용해야 할 사항이 있어 배포 했는데 소스가 이전 소스를 보고 있어서 CloudFront 설정을 확인했다.
- `Managed-CachingOptimized`로 설정되어 있다.
  - `MinTTL` 1 second.
  - `MaxTTL` 31,536,000 seconds (365 days).
  - `DefaultTTL` 86,400 seconds (24 hours).
  - 캐시 정책에 대해 참고 : https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-managed-cache-policies.html

## 캐시 삭제하기
- AWS 콘솔 - CloudFront - Distributions - 해당 아이템 선택
- Invalidations - Create Invalidation

![](.%5B20210428%5D_cloudfront_invalidating_objects_images/2f8e9881.png)

- 무효화 할 객체 경로를 적어주면 된다.
- 한 달 1,000건까지 무료, 이후에는 과금된다고 함.
- 더 자세한 내용은 아래 링크 참고.
  - https://aws.amazon.com/ko/premiumsupport/knowledge-center/cloudfront-serving-outdated-content-s3/#:~:text=Short%20description,the%20content%20in%20Amazon%20S3.
