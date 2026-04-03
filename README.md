@extends('layouts.profile')
@section('main')

<style>
  :root {
    --navy:        #1E3A5F;
    --navy-mid:    #2D4E78;
    --navy-light:  #EFF6FF;
    --accent:      #3B82F6;
    --accent-dark: #2563EB;
    --text-muted-blue: #6B8DB5;
    --border-blue: #DBEAFE;
  }

  .content-card {
    background: #fff;
    border: 1px solid var(--border-blue);
    border-radius: 1rem;
    padding: 1.25rem;
  }
  .content-card-title {
    color: var(--navy);
    font-size: .9rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: .4rem;
  }
  .edit-btn {
    background: none;
    border: none;
    color: var(--accent);
    font-size: .78rem;
    display: flex;
    align-items: center;
    gap: .25rem;
    cursor: pointer;
    padding: 0;
  }
  .edit-btn:hover { color: var(--accent-dark); }

  .info-tile {
    background: var(--navy-light);
    border-radius: .75rem;
    padding: .75rem;
  }
  .info-tile .label {
    color: var(--text-muted-blue);
    font-size: .72rem;
    margin-bottom: .15rem;
  }
  .info-tile .value {
    color: var(--navy);
    font-size: .875rem;
    font-weight: 600;
    word-break: break-all;
  }

  .sec-btn {
    width: 100%;
    text-align: left;
    border-radius: .75rem;
    padding: .75rem 1rem;
    font-size: .875rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border: 1px solid var(--border-blue);
    background: var(--navy-light);
    color: #334155;
    transition: background .18s;
    cursor: pointer;
  }
  .sec-btn:hover { background: var(--border-blue); }
  .sec-btn.danger {
    background: #fff1f2;
    border-color: #fecdd3;
    color: #f87171;
  }
  .sec-btn.danger:hover { background: #fee2e2; }

  /* Orders */
  .order-card {
    background: #fff;
    border: 1px solid var(--border-blue);
    border-radius: 1rem;
    padding: 1rem 1.25rem;
    transition: box-shadow .18s;
  }
  .order-card:hover { box-shadow: 0 4px 16px rgba(59,130,246,.1); }
  .order-id    { font-weight: 700; color: var(--navy); font-size: .9rem; }
  .order-date  { color: #94a3b8; font-size: .78rem; margin-top: .15rem; }
  .order-price { font-weight: 700; color: var(--accent); font-size: 1.05rem; }

  /* Wishlist */
  .wish-card {
    background: #fff;
    border: 1px solid var(--border-blue);
    border-radius: 1rem;
    padding: 1rem;
    height: 100%;
    transition: box-shadow .18s;
  }
  .wish-card:hover { box-shadow: 0 4px 16px rgba(59,130,246,.1); }
  .wish-name  { font-weight: 700; color: var(--navy); font-size: .88rem; margin-bottom: .35rem; }
  .wish-price { font-weight: 700; color: var(--accent); font-size: .95rem; margin-bottom: .75rem; }
  .wish-btn {
    width: 100%;
    background: var(--accent);
    color: #fff;
    border: none;
    border-radius: .6rem;
    padding: .45rem;
    font-size: .82rem;
    font-weight: 600;
    cursor: pointer;
    transition: background .18s;
  }
  .wish-btn:hover { background: var(--accent-dark); }

  /* Empty state */
  .empty-state {
    text-align: center;
    padding: 3rem 1rem;
    color: #94a3b8;
  }
  .empty-state i { font-size: 2.5rem; display: block; margin-bottom: .75rem; }
</style>

<div class="tab-content" id="accountTabContent">

  {{-- ═══════════════════════════════════════
       ORDERS
  ═══════════════════════════════════════ --}}
  <div class="tab-pane fade show active" id="orders" role="tabpanel">

    <h1 class="fw-bold fs-5 mb-4" style="color: var(--navy);">
      <i class="bi bi-box-seam me-2 text-primary"></i>My Orders
    </h1>

    @if(isset($orders) && count($orders) > 0)
      <div class="d-flex flex-column gap-3">
        @foreach($orders as $item)
          <div class="order-card">
            <div class="d-flex justify-content-between align-items-center">
              <div>
                <div class="order-id">ORD-{{ str_pad($item->id, 3, '0', STR_PAD_LEFT) }}</div>
                <div class="order-date">
                  <i class="bi bi-calendar3 me-1"></i>
                  {{ \Carbon\Carbon::parse($item->created_at)->format('M d, Y') }}
                </div>
              </div>
              <div class="text-end">
                <div class="order-price">₱{{ number_format($item->price, 2) }}</div>
                @if(isset($item->status))
                  @php
                    $statusClass = match($item->status) {
                      'Delivered'  => 'bg-success-subtle text-success',
                      'Shipped'    => 'bg-purple text-purple',
                      'Processing' => 'bg-primary-subtle text-primary',
                      'Pending'    => 'bg-warning-subtle text-warning',
                      'Cancelled'  => 'bg-danger-subtle text-danger',
                      default      => 'bg-secondary-subtle text-secondary',
                    };
                  @endphp
                  <span class="badge rounded-pill {{ $statusClass }} mt-1" style="font-size:.72rem;">
                    {{ $item->status }}
                  </span>
                @endif
              </div>
            </div>
          </div>
        @endforeach
      </div>
    @else
      <div class="empty-state">
        <i class="bi bi-inbox"></i>
        No orders yet. Start shopping!
      </div>
    @endif

  </div>

  {{-- ═══════════════════════════════════════
       WISHLIST
  ═══════════════════════════════════════ --}}
  <div class="tab-pane fade" id="wishlist" role="tabpanel">

    <h1 class="fw-bold fs-5 mb-4" style="color: var(--navy);">
      <i class="bi bi-heart me-2 text-primary"></i>My Wishlist
    </h1>

    @if(isset($wishlist) && count($wishlist) > 0)
      <div class="row g-3">
        @foreach($wishlist as $item)
          <div class="col-12 col-sm-6 col-lg-4">
            <div class="wish-card">
              <div class="wish-name">{{ $item->name }}</div>
              <div class="wish-price">₱{{ number_format($item->price, 2) }}</div>
              <a href="{{ route('product_detail', $item->id) }}" class="text-decoration-none">
                <button class="wish-btn">
                  <i class="bi bi-eye me-1"></i> View Item
                </button>
              </a>
            </div>
          </div>
        @endforeach
      </div>
    @else
      <div class="empty-state">
        <i class="bi bi-heart"></i>
        Your wishlist is empty.
      </div>
    @endif

  </div>

  {{-- ═══════════════════════════════════════
       SETTINGS
  ═══════════════════════════════════════ --}}
  <div class="tab-pane fade" id="settings" role="tabpanel">

    <h1 class="fw-bold fs-5 mb-4" style="color: var(--navy);">Account Settings</h1>

    <div class="d-flex flex-column gap-4">

      {{-- Personal Information --}}
      <div class="content-card">
        <div class="d-flex align-items-center justify-content-between mb-3">
          <div class="content-card-title">
            <i class="bi bi-person text-primary"></i> Personal Information
          </div>
          <button class="edit-btn">
            <i class="bi bi-pen"></i> Edit
          </button>
        </div>

        <div class="row g-2">
          <div class="col-6">
            <div class="info-tile">
              <div class="label">Full Name</div>
              <div class="value">{{ $user->first_name }} {{ $user->last_name }}</div>
            </div>
          </div>
          <div class="col-6">
            <div class="info-tile">
              <div class="label">Email</div>
              <div class="value">{{ $user->email }}</div>
            </div>
          </div>
          @if(isset($user->phone))
          <div class="col-6">
            <div class="info-tile">
              <div class="label">Phone</div>
              <div class="value">{{ $user->phone }}</div>
            </div>
          </div>
          @endif
          @if(isset($user->birthday))
          <div class="col-6">
            <div class="info-tile">
              <div class="label">Birthday</div>
              <div class="value">{{ \Carbon\Carbon::parse($user->birthday)->format('M d, Y') }}</div>
            </div>
          </div>
          @endif
        </div>
      </div>

      {{-- Security --}}
      <div class="content-card">
        <div class="content-card-title mb-3">
          🔒 Security
        </div>
        <div class="d-flex flex-column gap-2">
          <button class="sec-btn">
            Change Password
            <i class="bi bi-chevron-right"></i>
          </button>
          <button class="sec-btn danger">
            Delete Account
            <i class="bi bi-chevron-right"></i>
          </button>
        </div>
      </div>

    </div>
  </div>{{-- end settings --}}

</div>{{-- end tab-content --}}

@endsection
