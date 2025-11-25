[[마이크림 아키텍처 분석]]





personality_traits: PersonalityTraitsData | null; 추가
traits_completed_at: string | null; 추가


const traits = await InfluencerDB.getPersonalityTraits(influencerId);

이렇게 조회하시면 될 거 같습니다



