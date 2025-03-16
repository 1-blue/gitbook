# Frontend TsDoc Convention

### 📁 타입

> 모든 타입에 필수

* 장점
  1. `types/`에 있는 파일 자체가 더 상세한 API 문서가 됨
  2. 변수명만으로 유추하기 어려운 타입의 경우 조금 더 상세한 정보를 바로 확인할 수 있음
* 단점
  1. 코드가 늘어나서 불편할 수 있음
  2. 백엔드와 동기화되지 않는 경우 파악이 매우 어려워짐

```ts
/**
 * + 유저 채용관 승인 상태
 *   1. `review`: 검토중
 *   1. `needSupplement`: 권한 보충
 *   1. `approved`: 허용
 *   1. `noPermission`: 권한 없음
 **/
export type UserRecruitmentAdminApprovedStatus =
  | 'review'
  | 'needSupplement'
  | 'approved'
  | 'noPermission';

/**
 * + 유저 채용관 상태
 *   1. `none`:
 *   1. `member`: 멤버
 *   1. `manager`: 매니저
 *   1. `master`: 마스터
 *   1. `resign`: 퇴사자
 */
export type UserRecruitmentAdminStatus = 'none' | 'member' | 'manager' | 'master' | 'resign';

/** 유저 채용관 */
export interface UserRecruitmentAdmin {
  /** 유저 채용관 식별자 */
  id: number;
  /** 유저 채용관 유저 식별자 */
  userId: number;
  /** 유저 채용관 회사 식별자 */
  recruitmentCompanyId: number;
  /** 유저 채용관 휴대폰 번호 */
  phone: string;
  /** 유저 채용관 소속 */
  department: string;
  /** 유저 채용관 직급 */
  position: string;
  /** 유저 채용관 승인 상태 */
  approvedStatus: UserRecruitmentAdminApprovedStatus;
  /** 유저 채용관 상태 */
  status: UserRecruitmentAdminStatus;
  /** 유저 채용관 대표 마스터 여부 */
  isOriginMaster: false;
  /** 유저 채용관 TODO: ? */
  isBannerClosed: false;
  /** 유저 채용관 삭제 여부 */
  isDeleted: false;
  /** 유저 채용관 생성 시간 */
  createdAt: string;
  /** 유저 채용관 수정 시간 */
  updatedAt: string;
  /** 유저 채용관 회사 이름 */
  companyName: string;
  /** 유저 채용관 회사가 승인됐고, 서비스가 있는지 여부 */
  isCompanyCompleted: boolean;
  /** 유저 채용관 채용관 관리자가 마지막으로 본 채용 공고 식별자 */
  lastWatchedRecruitmentNoticeId: number;
}

/** 로그인된 유저 정보 타입 */
export interface UserInfoType {
  /** 유저 식별자 */
  id: number;
  /** 유저 이메일 */
  email: string;
  /** 유저 소셜 로그인 고유값 */
  externalId: string | null;
  /** 유저 채용관 정보 */
  recruitmentAdmin: UserRecruitmentAdmin | null;
}

export const loadloggedInfoAPI = () => axios.get<UserInfoType>('/api/v2/me');
(async () => {
  const user = await loadloggedInfoAPI();

  // 유저 채용관 정보
  // 유저 채용관 회사가 승인됐고, 서비스가 있는지 여부
  user.recruitmentAdmin.isCompanyCompleted
})()
```

### 🧱 컴포넌트

> * [MUI - Avatar](https://github.dev/mui/material-ui/tree/master)
> * [Antd - Avatar](https://github.com/ant-design/ant-design/blob/master/components/avatar/avatar.tsx)

> 공용으로 사용하는 컴포넌트에는 필수, 그 이외는 선택

* 장점
  1. 컴포넌트에 직접 들어가지 않아도 사용하는 부분에서 바로 `props`에 대한 정보를 알 수 있음
  2. 구체적으로 설명을 작성하다보면 더블 체크할 수 있음
  3. 만약 `Stortbook`을 사용한다면 자동적으로 컴포넌트와 `props`에 대한 설명이 기입됨
* 단점
  1. 컴포넌트가 오히려 더 길어짐

```tsx
interface Props {
  /**
   * 클래스명 ( `tailwindCss` )
   * @default ""
   */
  className?: string;
  /**
   * 둥글게 처리할지 여부
   * @default false
   */
  rounded?: boolean;

  /**
   * 아바타로 사용할 텍스트
   * @default ""
   */
  text?: string;
  /**
   * 아바타로 사용할 텍스트의 길이
   * @default ""
   */
  overflowTextLength?: number;
  /**
   * 아바타로 사용할 아이콘
   * @default undefined
   */
  icon?: React.ReactNode;
  /**
   * 아바타로 사용할 이미지 URL
   * @default ""
   */
  imagePath?: `https://${string}`;
}

/**
 * `framer-motion`과 `tailwindcss`를 사용하는 공용 아바타
 * ( 우선순위: `text` > `icon` > `imagePath` )
 *
 * @link [디자인 및 속성 참고 - Avatar(Antd)](https://ant.design/components/avatar)
 * @example
 * <Avatar text="김독자" />
 * <Avatar className="bg-main-500" icon={<HomeIcon />} />
 * <Avatar imagePath="https://avatars.githubusercontent.com/u/63289318?v=4" />
 *
 * @todo <Image />와 <img /> 분기처리하기
 */
const Avatar: React.FC<Props> = ({
  className = "",
  rounded = false,
  text = "",
  overflowTextLength = 1,
  icon,
  imagePath = "",
}) => {
  return (
    <figure></figure>
  );
};

export default Avatar;

// 사용하는 곳에서 마우스를 올리거나 자동완성할때 TsDoc에 작성한 설명이 출력됨
<Avatar imagePath="" />
```

### 🖌️ 커스텀 훅

> 공용으로 사용하는 커스텀 훅에는 필수, 그 이외는 선택
>
> * [레퍼런스 - usehooks-ts](https://github.com/juliencrn/usehooks-ts/tree/master/packages/usehooks-ts)

````tsx
import { useState } from 'react'

import type { RefObject } from 'react'

import { useEventListener } from '../useEventListener'

/**
 * Custom hook that tracks whether a DOM element is being hovered over.
 * @template T - The type of the DOM element. Defaults to `HTMLElement`.
 * @param {RefObject<T>} elementRef - The ref object for the DOM element to track.
 * @returns {boolean} A boolean value indicating whether the element is being hovered over.
 * @public
 * @see [Documentation](https://usehooks-ts.com/react-hook/use-hover)
 * @example
 * ```tsx
 * const buttonRef = useRef<HTMLButtonElement>(null);
 * const isHovered = useHover(buttonRef);
 * // Access the isHovered variable to determine if the button is being hovered over.
 * ```
 */
export function useHover<T extends HTMLElement = HTMLElement>(
  elementRef: RefObject<T>,
): boolean {
  const [value, setValue] = useState<boolean>(false)

  const handleMouseEnter = () => {
    setValue(true)
  }
  const handleMouseLeave = () => {
    setValue(false)
  }

  useEventListener('mouseenter', handleMouseEnter, elementRef)
  useEventListener('mouseleave', handleMouseLeave, elementRef)

  return value
}
````

### 🎀 데코레이터 활용

적절한 데코레이터가 있다면 사용하는게 좋을 것 같음`@deprecated`, `@example`는 유용하게 사용할 수 있을 것 같음

```ts
/**
 * 숫자 두개를 받아서 더하는 함수
 * 
 * @example
 * addNumber(1, 1); // 2
 * 
 * @link [미니인턴](https://miniintern.com)
 * 
 * @see 다른 참고할것들
 * 
 * // 안쓴다고 생각되는 컴포넌트/함수/타입 등에 작성해두고 테스트하고 삭제하는데 사용
 * @deprecated
 * 
 * // 기본 값이 있는 경우 명시
 * @defaultValue 10
 * 
 * // 타입스크립트라서 굳이 필요없지 않을까 생각함
 * // 매개변수나 리턴값에 대한 타입은 따로 만들어서 함수 자체의 타입으로 적용하는 방식이 좋지 않을까 생각함
 * @params
 * @returns
 **/
const addNumber = (a: number, b: number) => a + b;
```
