# import React,{ useState, useEffect } from 'react'

import React,{ useState, useEffect } from 'react'
import styled from 'styled-components';
import { useParams } from 'react-router-dom';

const ProductDetail = () => {

    const { productId } = useParams();
    const [product, setProduct] = useState(null);

    useEffect(() => {
        async function fetchProduct(){
            const response = await fetch(`https://port-0-express-server-17xco2nlsidlckv.sel5.cloudtype.app/products/${productId}`);
            const data = await response.json();
            setProduct(data.result);
        }
        fetchProduct();
    }, [productId]);

  return (
    <Section>
        {product === null ? (
            <p>상품 정보가 없습니다.</p>
        ) : (
            <>
                <ProductImage>
                    <Thumbnail *src*={product.imgSrc} *alt*="product thumbnail" />
                </ProductImage>
                
                <ProductContent>
                    <Brand>
                        {product.brand.nameKr} / &nbsp;
                        {product.brand.nameEn}
                    </Brand>
                    <Title>{product.name}</Title>
                    <InfoContainer>
                        <InfoRow>
                            <Label>정가</Label>
                            <Price>{product.originalPrice}</Price>
                        </InfoRow>
                        <InfoRow>
                            <Label>정가</Label>
                            <Price>{product.originalPrice}</Price>
                        </InfoRow>
                    </InfoContainer>
                </ProductContent>
            </>
        )}
    </Section>
  );
}

const Section = styled.section`
        padding: 1.5rem 1.25rem; // py-6, px-5
    @media (min-width: 1024px) { // lg:
        padding: 2.5rem 2rem; // py-10, px-8
    }
    margin: auto;
    max-width: 1024px; // max-w-screen-lg
    width: 100%;
    display: flex;
    flex-direction: row;
    align-items: stretch;
`;

const ProductImage = styled.div`
    width: 100%;
    max-width: 400px; // 예시로 추가한 값입니다.
    margin-right: 2rem; // 상품 이미지와 내용 사이의 간격을 위해 추가
`;

const ProductContent = styled.div`
    padding-top: 2rem; /* py-8 */
    padding-bottom: 2rem; /* py-8 */
    display: flex;
    flex-direction: column;
`;

const Thumbnail = styled.img`
    width: 100%;
    height: auto; // 이미지의 원본 비율을 유지하기 위해 추가
`;
const Brand = styled.div`
    font-size: 1rem;
    font-weight: bold;
`;
const Title = styled.div`
    font-size: 1.25rem;
    margin: 0.5rem 0;
`;
const InfoContainer = styled.div`
    font-size: 1rem;
    display: flex;
    flex-direction: column;
`;

const InfoRow = styled.div`
    display: flex;
    justify-content: start; // 좌측 정렬로 변경
    align-items: baseline; // 텍스트 기준선에 맞춤
    margin-bottom: 0.5rem; // 각 행 사이의 간격
`;

const Label = styled.span`
    font-size: 1rem;
    color: #333;
    margin-right: 0.5rem; // 라벨과 가격 사이 간격 추가
`;
const Price = styled.span`
  font-size: 1.5rem;
  color: '#333';
  text-decoration: line-through;
`;

export default ProductDetail
